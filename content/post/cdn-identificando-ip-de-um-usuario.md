+++
title = "CDN identificando ip de um usuario"
date = "2013-08-08"
draft = false
Categories = ["web performance", "portugues", "SL"]
Tags = ["portugues", "CDN", "web performance", "SL", "nginx", "apache"]
+++
Quando um site usa uma
[CDN](http://pt.wikipedia.org/wiki/Content_Delivery_Network) para fazer
cache e/ou aceleração as vantagens são bem conhecidas, mas algumas vezes
é necessário ajustar uma ou outra coisa para tudo continue funcionando.
Um exemplo é o servidor web do site deixa de receber requisições
diretamente do usuário porque agora tem os servidores da CDN
intermediando essa comunicação. Então, nos logs do servidor web estará
um IP de um servidor da CDN ao invés do IP de um usuário.


Para resolver esse problema, uitas CDNs enviam um cabeçalho HTTP extra
de suas requisições para o servidor web do site, esse cabeçalho é o
True-Client-IP.

Abaixo dois exemplos ([Apache](http://http.apache.org) e
[nginx](http://www.nginx.org)) de configuração do Log para registrar o
True-Client-IP.

#### Apache
```
[...]
  LogFormat "%v %h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" \"%{true}i\" %q" site.com

	CustomLog ${APACHE_LOG_DIR}/teste_access.log site.com   
[...]
```

#### nginx
```
[...]
  log_format teste '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_true_client_ip';

  access_log /var/log/nginx/teste.com.log site.com;
[...]
```
