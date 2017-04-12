---
categories: [ "portugues", "web peformance", "SL" ]
date: 2015-11-10T23:10:10-02:00
draft: false
description: [ "Identifcação de problemas básicos de desempenho de sites" ]
keywords: [ "web performance", "webpagetest", "rum", "gzip,front-end", "backend" ]
title: Identificando os gargalos de sites
Tags: ["portugues", "web performance", "webpagetest", "rum", "gzip", "ttfb", "front-end", "backend"]
---
![Web Performance](/images/320px-AMC_Javelins_1970_SST_and_Sunoco_at_car_show.jpg)

Este texto nasceu de um email de um amigo perguntando se existe algum material com o básico para identificar problemas de performance (gargalos) de sites. Não lembrei de nenhum, então segue alguns itens mais básicos que podem ajudar a encontrar porque um site está lento.

Web Performance é um tema vasto e muito variado, se tiver referências, correções ou mesmo dicas, comente ou mande email. :)
## Backend/Front-End

  No mundo internético, Backend é tudo que é processado pelo site (servidores web, banco de dados, APIs, etc). Front-end é tudo que é processado pelo navegador web.

  Isso é relativamente fácil identificar, a maioria dos serviços de testes de sites (monitoramento sintetico) usam a métrica TTFB (Time to First Byte). TTFB alto pode acontecer porque a infraestrutura do site está demorando para responder. Exemplo: Sites com páginas dinâmicas que precisam processar muita coisa para gerar a homepage de um site.  

  O TTFB alto também pode ser que o teste está sendo executando num local muito distante da infraestrutura do site. Exemplo disso é meu site ao ser testando no Brasil e nos EUA.

**Webpagetest - TTFB**

|  País  | Segundos |
|:--- |:---:|
| [EUA][1]    | 0,121s |
| [Brasil][2] | 0,325s |

[1]: http://www.webpagetest.org/result/151110_WJ_XE2/)
[2]: http://www.webpagetest.org/result/151110_MS_X5F/

  Isso acontece porque o servidor do meu site está no EUA, um número aceitável para um site que está nos EUA e os usuários no Brasil é em torno de 300 milissegundos.

  Se o site e os usuários estiverem nos EUA, o valor considerado bom é abaixo de 130 milissegundos.

### TTFB alto

  Pode ser várias coisas, um banco de dados com alto tempo de resposta, uma API conectada ao site terceiro, balanceador de carga com algoritimo errado, etc.

### SSL/TLS
  Um ponto que poucas pessoas verificam é a parte de criptografia (HTTPS). Já vi sites que o handshake de SSL/TLS para abrir a conexão HTTPS era próximo de 1 segundo, o recomendável deveria estar abaixo de 100 milissegundos.

*TLS/SSL do Github*
![SSL Github](/images/gargalo_ssl_github.png)

*TLS/SSL das listas do PostgreSQL Brasil*
![SSL PostgreSQL Brasil](/images/gargalo_ssl_pgbr.png)

  Incrível como no [teste com o Github](http://www.webpagetest.org/result/151110_RA_Z9A/1/details/) é rápido para fazer o handkshake SSL, contudo o mesmo [teste no site das listas de discussão do PostgreSQL Brasil](http://www.webpagetest.org/result/151110_G0_Z1S/1/details/) tem um desempenho sofrível (culpa minha!).

### DNS
  Parece incrível, contudo tem muito site que tem servidores DNS sofríveis em desempenho. Se a resolução DNS não for rápida (abaixo de 50 milissegundos), ele pode ser a causa do TTFB alto.

![DNS www.fernandoike.com](/images/gargalos_dns_fernandoike.png)

### Outros

  Como comentei um pouco mais acima, qualquer parte da infraestrutura de um site pode impactar no TTFB. Se estiver desconfiado que alguma na infraestrutura do site seja o gargalo, vale à pena considerar usar alguma coisa como New Relic para instrumentar os serviços e ver o que está enfileirando.

### Front-End

  Ainda que a causa seja a infraestrutura do site, só é possível identificar ao analisar com um navegador web.

Compressão (gzip)

  Qualquer resposta do servidor do site que for do tipo text/plain deve ser comprimida por gzip (RFC 2616). Eu escrevi um [texto](http://www.fernandoike.com/2014/12/23/configuracao-de-compressao-gzip-para-sites-e-ranking-de-cdn/) sobre isso no meu blog, recomendo lê-lo.



  Mas estiver com pressa (imagino que sim!), basicamente é o seguinte: se na resposta HTTP tiver o cabeçalho **Content-Type** com algum dos valores abaixo, deve-se considerar habilitar a compressão.

- **text/html**
- **application/x-javascript**
- **text/css**
- **application/javascript**
- **text/javascript**
- **text/plain**
- **text/xml**
- **application/json**
- **application/vnd.ms-fontobject**
- **application/x-font-opentype**
- **application/x-font-truetype**
- **application/x-font-ttf**
- **application/xml**
- **font/eot**
- **font/opentype**
- **font/otf**
- **image/svg+xml**
- **image/vnd.microsoft.icon**
- **text/x-js**

  O meu site (no momento) está com um [bom desempenho para compressão](http://www.webpagetest.org/result/151110_MS_X5F/1/performance_optimization/#compress_text) no Webpagetest.

![Gargalos gzip - nota](/images/gargalos_gzip1.png)

![Gargalos gzip - percentual](/images/gargalos_gzip2.png)

### Cache no navegador web (Cache-Control)

  O cabeçalho **Cache-Control** diz para o navegador web o que ele pode ou não cachear. O bom uso dele faz com que o site tenha um consumo menor de banda de rede. É muito comum usá-lo para fazer cache de imagens, javascripts, css e fontes no navegador web.

  O meu site não faz o bom uso dele [no teste](http://www.webpagetest.org/result/151110_MS_X5F/1/performance_optimization/#cache_static_content) que fiz no Webpagetest. Ao abrir o link abaixo você verá que a pontuação é baixa porque meu site usa conteúdo de terceiros (Linkedin e Slideshare), eles infelizmente não usam o Cache-Control.


  Ainda usando meu site como exemplo, se o Cache-Control fosse bem usado, a quantidade de requisições (request) HTTP no Repeat View seria bem menor. O Repeat View no meu blog tem 2/3 e ao menos deveria ser em abaixo de 40%.

#### Repeat View

  Simula o acesso de navegador web com parte do conteúdo cacheado pelo computador do usuário, seria como se o usuário acesse o site pela segunda vez.

![Cache-Control HTTP Header](/images/gargalo_cache_control.png)

### Terceiros

  Muitos sites usam conteúdo de terceiros nas suas páginas, geralmente conteúdo de redes sociais ou publicidade. Esse conteúdo por impactar no desempenho do site significativamente se for abusado o uso dele.

  Meu site tem mais requisições do Slideshare do que dele próprio, portanto, meu site é totalmente dependente do desempenho do Slideshare para ser rápido para usuário. Existem algumas formas de contornar usando coisas como **defer**.

  Como não vivo do site, posso conviver mas sites que são ecommerce ou portais de notícia não  podem conviver com esse "gargalo", precisam fazer que o as requisições HTTP para terceiros (parceiros) sejam feitas depois que Document Complete (ou o evento Onload) esteja concluído.

![Third Party HTTP Requests](/images/gargalo_third_party_requests.png)
