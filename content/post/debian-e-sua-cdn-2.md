+++
title = "Debian e sua CDN 2"
date = "2013-07-17"
draft = false
Categories = ["debian", "SL", "web performance"]
Tags = ["portugues", "CDN", "SL", "web performance", "debian"]
+++
Lembra do post
[anterior](http://www.fernandoike.com/2013/06/01/debian-e-sua-cdn-experimental/)
sobre a(s)
[CDN(s)](https://en.wikipedia.org/wiki/Content_delivery_network) do
[Debian](http://www.debian.org/)? Se não lembra ou não leu, vale ler
antes desse aqui. ;)

O anterior comentava um pouco do funcionamento da implantação do CDN
baseada em DNS. Dessa vez é comentar um pouco sobre outra “forma” de
CDN, esta é baseada em redirecionamento HTTP. A método para usuário é
simples, é apenas um redirecionamento (Código HTTP 302) para o local
onde o serviço identifica que o usuário terá melhor desempenho para
baixar os pacotes Debian.

Um teste simples realizado no Brasil.

```
    fike@klatoon:~$ curl -I http://http.debian.net/debian/
    HTTP/1.1 302 Moved Temporarily
    Date: Thu, 18 Jul 2013 01:25:40 GMT
    Server: Apache/2.2.16 (Debian)
    Vary: x-web-demo,Accept-Encoding
    X-IP: 179.186.50.212
    X-AS: 18881
    X-URL:
    X-Arch:
    X-Country: BR
    X-Continent: SA
    X-Std-Dev: 12.0185273640326
    X-Population: 4
    X-Closest-Distance: 0
    X-Distance: 0
    X-Match-Type: country
    Link: ; rel=duplicate; pri=1; depth=0, ; rel=duplicate; pri=1; depth=0
    Location: http://debian.c3sl.ufpr.br/debian/
    Content-Type: text/plain
```

Na resposta do servidor a requisição realizado pelo **curl** tem vários
cabeçalhos que ajudam entender o funcionamento. O servidor do
**http.debian.net** identifica o IP de origem da requisição, o país, o [Autonomous
System](https://en.wikipedia.org/wiki/Autonomous_System_(Internet))
(AS), etc. Ao final tem o cabeçalho **Location** apontando qual será a
URL que responderá a requisição.

Abaixo o mesmo teste mas realizado nos EUA.

    fike@midstorm:~$ curl -I http://http.debian.net/debian/
    HTTP/1.1 302 Moved Temporarily
    Date: Thu, 18 Jul 2013 01:26:07 GMT
    Server: Apache/2.2.16 (Debian)
    Vary: x-web-demo,Accept-Encoding
    X-IP: 74.50.55.64
    X-AS: 36024
    X-URL:
    X-Arch:
    X-Country: US
    X-Continent: NA
    X-Std-Dev: 3.5960358730135
    X-Population: 15
    X-Closest-Distance: 13.434
    X-Distance: 13.434
    X-Match-Type: country
    Location: http://debian.gtisc.gatech.edu/debian/
    Content-Type: text/plain

Interessante que no teste dos EUA tem um pouco mais de informações que
melhoram a escolha do melhor espelho (mirror) do repositório Debian para
para a requisição.

Se quiser conhecer um pouco mais pode entrar na [página do
projeto](https://github.com/rgeissert/http-redirector/) no
[Github](http://github.com). Ele bem simples e o [Raphael
Geissert](http://rgeissert.blogspot.com.br/) ficará feliz com
informações de bugs, patches, etc. ;)

Ah! Já estava esquecendo, se quiser testá-lo, basta adicionar uma linha
no */etc/apt/sources.list*. No meu caso estou usando para o
[Sid/Unstable](http://www.debian.org/releases/sid/).

```
deb [arch=amd64,i386] http://http.debian.net/debian/ unstable main contrib non-free
```
