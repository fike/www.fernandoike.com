+++
title = "Configuracao de compressao gzip para sites e ranking de CDN"
date = "2014-12-23"
draft = false
Categories = ["portugues", "web performance", "FEO", "CDN", "SL"]
Tags = ["portugues", "FEO", "CDN", "webpagetest", "http archive"]
+++
Estava lendo um [texto](http://www.fastly.com/blog/new-gzip-settings-and-deciding-what-to-compress/) do Steve Souders sobre a alteração da configuração padrão gzip na Fastly. Fastly é uma CDN concorrente da Akamai e tem clientes como Twitter, Shopify, The Guardian, Rakuten, etc.

Ele cita como chegaram no template padrão da configuração deles usando os dados do [HTTP Archive](http://httparchive.org/), este é um projeto que consolida testes executados usando a versão pública do [Webpagetest](http://www.webpagetest.org/). Os testes são executados em mais ou menos 18 mil URLs e tem [relatórios](http://httparchive.org/trends.php) variados, por exemplo: número médio de requisições HTTP por página, crescimento do HTML nas páginas, etc.

Tanto do Steve Souders quanto no site HTTP Archive fazem referência ao [Bigqueries](http://httparchive.org/) com diversas consultas realizadas na base dados do HTTP Archive. Um [texto postado](http://bigqueri.es/t/top-base-page-cdns-for-top-urls/58) no Bigqueries chamou-me a atenção, era sobre o Ranking de CDNs considerandos as páginas mais populares.

![]( /images/image_0.png)

Ele considerou apenas as páginas que estavam sendo entregues por alguma CDN e não considerou todas as requisições HTTP das páginas. Usei o BigQuery do Google considerando os dados disponíveis do HTTP Archive no mês de Novembro de 2014 para responder: Quais são as CDNs mais populares ao analisar as requisições HTTP?

```
SELECT cdn, num, ROUND(ratio*100) as percent FROM (
  SELECT cdn, COUNT(cdn) as num, RATIO_TO_REPORT(num) OVER() ratio   FROM (
     SELECT CASE
       WHEN _cdn_provider IN ('')
         THEN 'None'
         ELSE 'CDN'
       END as cdn
      FROM httparchive:runs.2014_11_01_requests,
           httparchive:runs.2014_11_15_requests,
           httparchive:runs.2014_11_01_requests_mobile,
           httparchive:runs.2014_11_15_requests_mobile
   ) GROUP BY cdn
) ORDER BY percent DESC
```

![]( /images/image_1.png)

E quais foram as CDNs mais usadas naquele período?

```
SELECT provider, round(100*ratio) as percent, num
FROM (SELECT REGEXP_REPLACE(_cdn_provider,r'^$', 'None') as provider, count(*) as num, RATIO_TO_REPORT(num) OVER() ratio
 FROM httparchive:runs.2014_11_01_requests,
      httparchive:runs.2014_11_15_requests,
      httparchive:runs.2014_11_01_requests_mobile,
      httparchive:runs.2014_11_15_requests_mobile
 WHERE  _cdn_provider != ''
GROUP BY provider
)
ORDER BY num desc LIMIT 10

```

![]( /images/image_2.png)

A surpresa no ranking é o Google, porque ele seria considerado uma CDN?

Para tentar entender, outra consulta buscando os principais hostnames/domínios que estão na CDN do Google.

```
SELECT req_host, count(req_host) as num
FROM httparchive:runs.2014_11_01_requests,
     httparchive:runs.2014_11_15_requests,
     httparchive:runs.2014_11_01_requests_mobile,
     httparchive:runs.2014_11_15_requests_mobile
WHERE _cdn_provider = 'Google'
GROUP BY req_host
ORDER BY num DESC
LIMIT 20
```

![]( /images/image_3.png)

Basicamente, a CDN da Google entrega seus próprios serviços: Analytics, Adsense, Doubleclick, Youtube, etc. Os hostnames fonts.googleapis.com, ajax.googleapis.com estão relacionados a iniciativas do Goolgle de hospedar alguns frameworks javascripts e webfonts gratuitamente.

Então, o Google poderia ser considerado um fornecedor de CDN? Um pouco difícil de definir porque não existe um documento canonical (*RFC*) que defina CDN. A Wikipedia tem artigo sobre CDN e a primeira frase tem uma boa definição

“A *content delivery network* or *content distribution network* (CDN) is a large distributed system of servers deployed in multiple data centers across the Internet. The goal of a CDN is to serve content to end-users with high availability and high performance. CDNs serve a large fraction of the Internet content today, including web objects (text, graphics and scripts), downloadable objects (media files, software, documents), applications (e-commerce, portals), live streaming media, on-demand streaming media, and social networks.*"

Se a for usado a definição da Wikipedia para CDN, pode-se afirmar que alguns serviços do Google são uma CDN. Entretanto, se descartar o Google como CDN e consideramos que as demais restantes são CDNs que seus usuários paguem para entregar o seu conteúdo. Como ficaria o ranking com as 15 mais usadas?

```
SELECT provider, round(100*ratio) as percent, num
FROM (SELECT REGEXP_REPLACE(_cdn_provider,r'^$', 'None') as provider, count(*) as num, RATIO_TO_REPORT(num) OVER() ratio
  FROM httparchive:runs.2014_11_01_requests,
       httparchive:runs.2014_11_15_requests,
       httparchive:runs.2014_11_01_requests_mobile,
       httparchive:runs.2014_11_15_requests_mobile
  WHERE _cdn_provider != 'Google' AND _cdn_provider != ''
GROUP BY provider
)
ORDER BY num desc
```

![]( /images/image_4.png)

Dentre as acima listadas, as que tem ou tera ponto de presença no Brasil: Akamai, Cloudflare, EdgeCast, CloudFront, Fastly, MaxCDN (NetDNA), CDNetwokrs, ChinaNetCenter, Level3, Incapsula e Highwinds.

Voltando ao início e aoEu texto do Souders sobre compressão, ele propôs que habilite/configure a compressão quando as respostas HTTP tiverem :

*Extensions* : *js css html json ico eot otf ttf

Ou

*Content-types*: *text/html application/x-javascript text/css application/javascript text/javascript text/plain text/xml  application/json  application/vnd.ms-fontobject application/x-font-opentype application/x-font-truetype application/x-font-ttf application/xml font/eot font/opentype font/otf image/svg+xml image/vnd.microsoft.icon

*A configuração padrão na Akamai é*:

*Content-types* : *text/html* text/css* application/x-javascript* text/xml* text/plain* application/json* text/javascript*

Fazendo consulta similar ao do Souders para saber "Quais os content-types mais mais recorrentes acima de 1 mil recorrências e que tiveram compressão habilitada?".

```
SELECT content_type, round(100*ratio) as percent, num
FROM
  (SELECT count(resp_content_type) as num,
    REGEXP_REPLACE(resp_content_type,r';.*', '') as content_type, RATIO_TO_REPORT(num) OVER() ratio
    FROM httparchive:runs.2014_11_01_requests
    WHERE NOT (resp_content_type contains 'image' OR resp_content_type contains 'audio' OR resp_content_type = '') AND _gzip_save > 0
    GROUP BY content_type HAVING num > 1000)
ORDER BY num DESC;
```

![]( /images/tab_content_type_percent.png)

Da lista, pode-se descartar alguns: *application/octet-stream* (formato genérico de arquivos), *text/x-component* (formato microsoft antigo, não mais usado), *application/x-shockwave-flash*, *font/woff* e *application/x-www-form-urlencoded*.  Os três últimos são formatos já com compressão e fazer compressão num servidor web ou CDN é usar o processamento desnecessariamente.

Juntado as listas, a regra a ser configurado no servidor web, proxy reverso ou CDN será:

**Extensions**: *js css html json ico eot otf ttf*

**Content-Type**: *text/html application/x-javascript text/css application/javascript text/javascript text/plain text/xml  application/json  application/vnd.ms-fontobject application/x-font-opentype application/x-font-truetype application/x-font-ttf application/xml font/eot font/opentype font/otf image/svg+xml image/vnd.microsoft.icon* **text/x-js**.

Acrescentado o **text/x-js** na lista de Content-Type, um site poderá ter mais requisições HTTP compressão, consequentemente o site terá o tráfego de rede menor. Claro, sem esquecer de mencionar que o usuário poderá ter uma experência melhor com as páginas do site já que elas poderão ser menores e mais rápidas.

Nas novas configurações na Akamai estou acrescentando os Content-Type e os arquivos para as regras de compressão e cache como abaixo:

## Regra de compressão

![]( /images/image_5.png)

## Regra de Cache

![]( /images/image_6.png)

Os resultados e comentários sobre ranking das CDNs estão no [texto](http://bigqueri.es/t/whats-the-popularity-of-different-cdns/477/2) que [publiquei](http://bigqueri.es/t/whats-the-popularity-of-different-cdns/477/2) publicado no Bigqueries.

Obs.: As expressões regulares no BigQuery são baseadas no **RE2**, recomendo fortemente ler a [documentação dele](https://code.google.com/p/re2/wiki/Syntax).


## Links

[http://httparchive.org/](http://httparchive.org/)

[http://httparchive.org/trends.php](http://httparchive.org/trends.php)

[http://en.wikipedia.org/wiki/Content_delivery_network](http://en.wikipedia.org/wiki/Content_delivery_network)

[http://www.fastly.com/blog/new-gzip-settings-and-deciding-what-to-compress/](http://www.fastly.com/blog/new-gzip-settings-and-deciding-what-to-compress/)

[http://bigqueri.es/t/whats-the-popularity-of-different-cdns/477](http://bigqueri.es/t/whats-the-popularity-of-different-cdns/477)

[https://cloud.google.com/bigquery/query-reference](https://cloud.google.com/bigquery/query-reference)

[https://code.google.com/p/re2/wiki/Syntax](https://code.google.com/p/re2/wiki/Syntax)
