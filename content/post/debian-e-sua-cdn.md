+++
title = "Debian e sua cdn"
date = "2013-06-01"
draft = false
Categories = ["debian", "web performance", "SL","portugues"]
Tags = ["portugues", "debian", "cdn", "web performance", "SL"]
+++
Esse post nasceu de uma
[discussão](https://www.facebook.com/eribertomota/posts/10200459836833517?comment_id=5113409&offset=0&total_comments=20&notif_t=share_reply)
no Facebook sobre um dos projetos de
[CDN](http://wiki.debian.org/DebianGeoMirror) em teste no Debian. Um
deles é a [cdn.debian.net](http://cdn.debian.net/) e o outro é o
[http.debian.net](http://http.debian.net/).

Testar ambos projetos não precisa de muito trabalho basta acrescentar ou
alterar o sources.list:

    deb http://http.debian.net/debian stable main

Ou:

    deb http://cdn.debian.net/debian stable main

O funcionamento dos dois é levemente diferente, o cdn.debian.net é
baseado em [geoDNS](http://www.caraytech.com/geodns/) e o
http.debian.net tem uma proposta um pouco mais sofisticada. O teste
abaixo é para o cdn.debian.net mas se quiser testar o http.debian.net
pode testar o [demo](http://http.debian.net/demo.html).

No Brasil, o servidor da cdn.debian.net mapeado é o **200.19.252.56** e
pode verficar usando o **dig**.

```
$dig cdn.debian.net

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> cdn.debian.net
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1245
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;cdn.debian.net.          IN  A

;; ANSWER SECTION:
cdn.debian.net.       3021    IN  CNAME   deb.cdn.araki.net.
deb.cdn.araki.net.    6   IN  A   200.19.252.56

;; Query time: 17 msec
;; SERVER: 200.175.5.139#53(200.175.5.139)
;; WHEN: Fri May 31 23:45:47 2013
;; MSG SIZE  rcvd: 76
```

Descoberto o IP do servidor é testar se responde corretamente:

    $curl -I -H "Host:cdn.debian.net" http://200.19.252.56/debian/
    HTTP/1.1 200 OK
    Date: Sat, 01 Jun 2013 02:59:00 GMT
    Server: Apache/2.2.11 (Ubuntu) PHP/5.2.6-3ubuntu4.5 with Suhosin-Patch
    Content-Type: text/html;charset=UTF-8

Olha que interessante, o servidor do repositório **Debian** é um
**Ubuntu**. Não que isso seja um problema, poderia ser um Sistema
Operacional proprietário, o mais importante para uma
[CDN](https://en.wikipedia.org/wiki/Content_delivery_network) como esta
é disponibilidade de recurso (armazenamento dos pacotes e banda). ;)

Vamos testar outro servidor, um que esteja foda da América do Sul, para
isso devemos recorrer novamente ao **dig** mas fazendo a consulta em um
servidor DNS em outro continente como é o DNS público do Google.

    root@klatoon:~# dig cdn.debian.net @8.8.8.8

    ; > DiG 9.8.4-rpz2+rl005.12-P1 > cdn.debian.net @8.8.8.8
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER


    O retorno do dig é um IP diferente, agora retornou 128.30.2.36, vamos
    testar o retorno do servidor com curl novamente.



    fike@klatoon:~$ curl -H "Host:cdn.debian.net" http://128.30.2.36/debian/pool


    301 Moved Permanently

    Moved Permanently
    The document has moved here.

    Apache/2.2.16 (Debian) Server at cdn.debian.net Port 80

Hum… Agora o servidor respondeu como sendo um Debian. ;)
