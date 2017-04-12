+++
title = "Algumas opcoes do dig"
date = "2013-05-20"
Categories = ["debian", "portugues"]
Tags = ["portugues", "debian", "dig", "dns"]
+++
Muitas pessoas gostam de usar o **nslookup** para pesquisar informação
de DNS. Eu, particularmente eu prefiro usar o **dig** e logo mais abaixo
tem algumas opções se você tiver interesse em usá-lo. ;)

Como fazer uma consulta sobre o reverso de endereço de rede (IP):

```
$ dig -x 8.8.8.8

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6197
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.        IN  PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa. 41387   IN  PTR google-public-dns-a.google.com.

;; Query time: 223 msec
;; SERVER: 200.175.5.139#53(200.175.5.139)
;; WHEN: Fri May 17 22:54:23 2013
;; MSG SIZE  rcvd: 82
```

No caso acima o DNS reverso para o endereço de rede **8.8.8.8** é
**google-public-dns-a.google.com**. Porém, se quisermos saber o(s)
servidor(es) de email de um domínio?

```
dig mx gmail.com

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> mx gmail.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1486
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 8

;; QUESTION SECTION:
;gmail.com.           IN  MX

;; ANSWER SECTION:
gmail.com.        2851    IN  MX  40 alt4.gmail-smtp-in.l.google.com.
gmail.com.        2851    IN  MX  20 alt2.gmail-smtp-in.l.google.com.
gmail.com.        2851    IN  MX  5 gmail-smtp-in.l.google.com.
gmail.com.        2851    IN  MX  30 alt3.gmail-smtp-in.l.google.com.
gmail.com.        2851    IN  MX  10 alt1.gmail-smtp-in.l.google.com.

;; ADDITIONAL SECTION:
gmail-smtp-in.l.google.com. 197   IN  A   74.125.140.27
gmail-smtp-in.l.google.com. 259   IN  AAAA    2607:f8b0:4002:c04::1b
alt3.gmail-smtp-in.l.google.com. 44 IN    A   173.194.65.26
alt3.gmail-smtp-in.l.google.com. 62 IN    AAAA    2a00:1450:4013:c00::1b
alt1.gmail-smtp-in.l.google.com. 267 IN   A   173.194.73.27
alt1.gmail-smtp-in.l.google.com. 171 IN   AAAA    2607:f8b0:400c:c02::1a
alt4.gmail-smtp-in.l.google.com. 190 IN   A   173.194.70.27
alt4.gmail-smtp-in.l.google.com. 31 IN    AAAA    2a00:1450:4001:c02::1a

;; Query time: 17 msec
;; SERVER: 200.175.5.139#53(200.175.5.139)
;; WHEN: Fri May 17 23:03:30 2013
;; MSG SIZE  rcvd: 326
```

Consultar os servidores DNS de um domínio?

```
$dig NS gmail.com

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> NS gmail.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15754
;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 4

;; QUESTION SECTION:
;gmail.com.           IN  NS

;; ANSWER SECTION:
gmail.com.        337395  IN  NS  ns2.google.com.
gmail.com.        337395  IN  NS  ns4.google.com.
gmail.com.        337395  IN  NS  ns3.google.com.
gmail.com.        337395  IN  NS  ns1.google.com.

;; ADDITIONAL SECTION:
ns4.google.com.       299858  IN  A   216.239.38.10
ns3.google.com.       299798  IN  A   216.239.36.10
ns1.google.com.       299798  IN  A   216.239.32.10
ns2.google.com.       299824  IN  A   216.239.34.10

;; Query time: 21 msec
;; SERVER: 200.175.5.139#53(200.175.5.139)
;; WHEN: Fri May 17 23:07:04 2013
;; MSG SIZE  rcvd: 170
```

Consultar um servidor DNS responsável por um domínio?

```
$dig A www.google.com.br @ns1.google.com

; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> A www.google.com.br @ns1.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 53502
;; flags: qr aa rd; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;www.google.com.br.       IN  A

;; ANSWER SECTION:
www.google.com.br.    300 IN  A   74.125.234.87
www.google.com.br.    300 IN  A   74.125.234.88
www.google.com.br.    300 IN  A   74.125.234.95

;; Query time: 12 msec
;; SERVER: 216.239.32.10#53(216.239.32.10)
;; WHEN: Fri May 17 23:11:23 2013
;; MSG SIZE  rcvd: 83
```

Obter somente a(s) linha(s) com a resposta

```
$dig www.google.com +nocomments +noquestion +noauthority +noadditional +nostats

; <<>> DiG 9.9.5-7-Debian <<>> www.google.com +nocomments +noquestion +noauthority +noadditional +nostats
;; global options: +cmd
www.google.com.		61	IN	A	173.194.118.144
www.google.com.		61	IN	A	173.194.118.145
www.google.com.		61	IN	A	173.194.118.146
www.google.com.		61	IN	A	173.194.118.147
www.google.com.		61	IN	A	173.194.118.148
```


Para saber mais… ;)

```
$man dig
```
