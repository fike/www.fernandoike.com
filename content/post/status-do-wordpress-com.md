+++
title = "Status do wordpress com"
date = "2012-10-15"
draft = false
Categories = ["monitoramento", "portugues"]
Tags = ["portugues", "wordpress", "monitoramento", "curl"]
+++
O [Wordpress](http://wordpress.org/) é provavelmente a maior plataforma
de blog existente na atualidade. Maior, entenda-se  como a mais usada.
 O [wordpress.com](http://wordpress.com) é a versão de código-aberto com
algumas funcionalidade extras, sendo que algumas dessas funcionalidades
são pagas.

Não que isso seja um problema, muito pelo contrátrio. Afinal, como já
dizem por aí: “Não existe almoço grátis!”

Na [página de status](http://en.wordpress.com/stats/) deles tem um mapa
que mostra as atualizações (post, comentários, etc…) na plataforma.

![](http://farm9.staticflickr.com/8054/8092213914_420f7c8efa_z.jpg) Os
números deles são bem interessantes: **373 milhões** de visitantes por
mês, **500 mil post** e **400 comentário**s todos os dias. Entre os 10
maiores idiomas usados estão **Português**, **Indonésio** e **Vietnã**.

Ah!!! Já estava me esquecendo! No topo mostra a soma de todos os sites
que usam wordpress: **56 milhões**.

Também não posso deixar de mencionar que eles mantém a infraestrutura
para suportar todos esses números com um pouco mais de **150
funcionários**.

Obs. Faça um teste em qual sites deles para ver os cabeçalhos HTTP com
[curl](http://curl.haxx.se/), vai achar um easter egg bem interessante.
;)

Obs. Faça um teste em qual sites deles para ver os cabeçalhos HTTP com
[curl](http://curl.haxx.se/), vai achar um easter egg bem interessante.
;)

```
$curl -I http://wordpress.com
```
