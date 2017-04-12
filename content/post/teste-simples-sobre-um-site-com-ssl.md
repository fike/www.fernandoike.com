+++
title = "Teste simples sobre um site com ssl"
date = "2013-01-04"
draft = false
Categories = ["SL", "debian", "portugues"]
Tags = ["portugues", "SL", "debian", "openssl"]
+++
O título é péssimo mas por falta de inspiração fica esse por enquanto.

Estava precisando testar de uma maneira mais simples alguns servidores
web com [SSL](http://en.wikipedia.org/wiki/SSL). Anteriormente estava
testando manualmente os servidores com o **openssl** até descobrir o
[**sslscan**](https://www.titania-security.com/labs/sslscan).

O sslscan testa automaticamente as versões de protocolo (**SSLv2**,
**SSLv3**, **TLS 1.0**, etc.), como também testa o tipo de chave
criptográfica (cipher) suportado. Ele é muito mais simples do que criar
um script usando [openssl](http://www.openssl.org/):

```
echo -n | openssl s_client -ssl3 -connect www.site.com:443
    CONNECTED(00000003)
    depth=1 C = ZA, O = Thawte Consulting (Pty) Ltd., CN = Thawte SGC CA
    verify error:num=20:unable to get local issuer certificate
    verify return:0
    ---
    Certificate chain
     [...]
    ---
    Server certificate
    -----BEGIN CERTIFICATE-----
    [...]
    ---
    No client certificate CA names sent
    ---
    SSL handshake has read 2005 bytes and written 297 bytes
    ---
    New, TLSv1/SSLv3, Cipher is ECDHE-RSA-RC4-SHA
    Server public key is 1024 bit
    Secure Renegotiation IS supported
    Compression: NONE
    Expansion: NONE
    SSL-Session:
     Protocol : SSLv3
     Cipher : ECDHE-RSA-RC4-SHA
     Session-ID: 7F390B960A723A139C4A714F1086A23F1B43670D4C3B9604C7251400DAE9DE9F
     Session-ID-ctx:
     Master-Key: D4FE8112BD1CDF58C3329996009E21133946ADD85BB168621599846523AC018F08AC2CFC331BA5A7C8F38C9F74AF1810
     Key-Arg : None
     PSK identity: None
     PSK identity hint: None
     SRP username: None
     Start Time: 1357299783
     Timeout : 7200 (sec)
     Verify return code: 20 (unable to get local issuer certificate)
    ---
    DONE
```

O mesmo teste usando sslscan:

```
$ sslscan www.site.com
     _
     ___ ___| |___ ___ __ _ _ __
     / __/ __| / __|/ __/ _` | '_ \
     \__ \__ \ \__ \ (_| (_| | | | |
     |___/___/_|___/\___\__,_|_| |_|
    Version 1.8.2

    http://www.titania.co.uk

     Copyright Ian Ventura-Whiting 2009
    Testing SSL server www.site.com on port 443
    Supported Server Cipher(s):
     Failed SSLv3 256 bits ECDHE-RSA-AES256-GCM-SHA384
     Failed SSLv3 256 bits ECDHE-ECDSA-AES256-GCM-SHA384
     Failed SSLv3 256 bits ECDHE-RSA-AES256-SHA384
     Failed SSLv3 256 bits ECDHE-ECDSA-AES256-SHA384
     Accepted SSLv3 256 bits ECDHE-RSA-AES256-SHA
     Rejected SSLv3 256 bits ECDHE-ECDSA-AES256-SHA
     Rejected SSLv3 256 bits SRP-DSS-AES-256-CBC-SHA
     Rejected SSLv3 256 bits SRP-RSA-AES-256-CBC-SHA
     Failed SSLv3 256 bits DHE-DSS-AES256-GCM-SHA384
     Failed SSLv3 256 bits DHE-RSA-AES256-GCM-SHA384
     Failed SSLv3 256 bits DHE-RSA-AES256-SHA256
     Failed SSLv3 256 bits DHE-DSS-AES256-SHA256
     Rejected SSLv3 256 bits DHE-RSA-AES256-SHA
     Rejected SSLv3 256 bits DHE-DSS-AES256-SHA
     Rejected SSLv3 256 bits DHE-RSA-CAMELLIA256-SHA
     Rejected SSLv3 256 bits DHE-DSS-CAMELLIA256-SHA
     Rejected SSLv3 256 bits AECDH-AES256-SHA
     Rejected SSLv3 256 bits SRP-AES-256-CBC-SHA
     Failed SSLv3 256 bits ADH-AES256-GCM-SHA384
     Failed SSLv3 256 bits ADH-AES256-SHA256
     Rejected SSLv3 256 bits ADH-AES256-SHA
     Rejected SSLv3 256 bits ADH-CAMELLIA256-SHA
     Failed SSLv3 256 bits ECDH-RSA-AES256-GCM-SHA384
     Failed SSLv3 256 bits ECDH-ECDSA-AES256-GCM-SHA384
     Failed SSLv3 256 bits ECDH-RSA-AES256-SHA384
     Failed SSLv3 256 bits ECDH-ECDSA-AES256-SHA384
     Rejected SSLv3 256 bits ECDH-RSA-AES256-SHA
     Rejected SSLv3 256 bits ECDH-ECDSA-AES256-SHA
     Failed SSLv3 256 bits AES256-GCM-SHA384
     Failed SSLv3 256 bits AES256-SHA256
     Accepted SSLv3 256 bits AES256-SHA
     Rejected SSLv3 256 bits CAMELLIA256-SHA
     Failed SSLv3 256 bits PSK-AES256-CBC-SHA
     Accepted SSLv3 168 bits ECDHE-RSA-DES-CBC3-SHA
     Rejected SSLv3 168 bits ECDHE-ECDSA-DES-CBC3-SHA
     Rejected SSLv3 168 bits SRP-DSS-3DES-EDE-CBC-SHA
     Rejected SSLv3 168 bits SRP-RSA-3DES-EDE-CBC-SHA
     Rejected SSLv3 168 bits EDH-RSA-DES-CBC3-SHA
     Rejected SSLv3 168 bits EDH-DSS-DES-CBC3-SHA
     Rejected SSLv3 168 bits AECDH-DES-CBC3-SHA
     Rejected SSLv3 168 bits SRP-3DES-EDE-CBC-SHA
     Rejected SSLv3 168 bits ADH-DES-CBC3-SHA
     Rejected SSLv3 168 bits ECDH-RSA-DES-CBC3-SHA
     Rejected SSLv3 168 bits ECDH-ECDSA-DES-CBC3-SHA
     Accepted SSLv3 168 bits DES-CBC3-SHA
     Failed SSLv3 168 bits PSK-3DES-EDE-CBC-SHA
     Failed SSLv3 128 bits ECDHE-RSA-AES128-GCM-SHA256
     Failed SSLv3 128 bits ECDHE-ECDSA-AES128-GCM-SHA256
     Failed SSLv3 128 bits ECDHE-RSA-AES128-SHA256
     Failed SSLv3 128 bits ECDHE-ECDSA-AES128-SHA256
     Accepted SSLv3 128 bits ECDHE-RSA-AES128-SHA
     Rejected SSLv3 128 bits ECDHE-ECDSA-AES128-SHA
     Rejected SSLv3 128 bits SRP-DSS-AES-128-CBC-SHA
     Rejected SSLv3 128 bits SRP-RSA-AES-128-CBC-SHA
     Failed SSLv3 128 bits DHE-DSS-AES128-GCM-SHA256
     Failed SSLv3 128 bits DHE-RSA-AES128-GCM-SHA256
     Failed SSLv3 128 bits DHE-RSA-AES128-SHA256
     Failed SSLv3 128 bits DHE-DSS-AES128-SHA256
     Rejected SSLv3 128 bits DHE-RSA-AES128-SHA
     Rejected SSLv3 128 bits DHE-DSS-AES128-SHA
     Rejected SSLv3 128 bits DHE-RSA-SEED-SHA
     Rejected SSLv3 128 bits DHE-DSS-SEED-SHA
     Rejected SSLv3 128 bits DHE-RSA-CAMELLIA128-SHA
     Rejected SSLv3 128 bits DHE-DSS-CAMELLIA128-SHA
     Rejected SSLv3 128 bits AECDH-AES128-SHA
     Rejected SSLv3 128 bits SRP-AES-128-CBC-SHA
     Failed SSLv3 128 bits ADH-AES128-GCM-SHA256
     Failed SSLv3 128 bits ADH-AES128-SHA256
     Rejected SSLv3 128 bits ADH-AES128-SHA
     Rejected SSLv3 128 bits ADH-SEED-SHA
     Rejected SSLv3 128 bits ADH-CAMELLIA128-SHA
     Failed SSLv3 128 bits ECDH-RSA-AES128-GCM-SHA256
     Failed SSLv3 128 bits ECDH-ECDSA-AES128-GCM-SHA256
     Failed SSLv3 128 bits ECDH-RSA-AES128-SHA256
     Failed SSLv3 128 bits ECDH-ECDSA-AES128-SHA256
     Rejected SSLv3 128 bits ECDH-RSA-AES128-SHA
     Rejected SSLv3 128 bits ECDH-ECDSA-AES128-SHA
     Failed SSLv3 128 bits AES128-GCM-SHA256
     Failed SSLv3 128 bits AES128-SHA256
     Accepted SSLv3 128 bits AES128-SHA
     Rejected SSLv3 128 bits SEED-SHA
     Rejected SSLv3 128 bits CAMELLIA128-SHA
     Failed SSLv3 128 bits PSK-AES128-CBC-SHA
     Accepted SSLv3 128 bits ECDHE-RSA-RC4-SHA
     Rejected SSLv3 128 bits ECDHE-ECDSA-RC4-SHA
     Rejected SSLv3 128 bits AECDH-RC4-SHA
     Rejected SSLv3 128 bits ADH-RC4-MD5
     Rejected SSLv3 128 bits ECDH-RSA-RC4-SHA
     Rejected SSLv3 128 bits ECDH-ECDSA-RC4-SHA
     Accepted SSLv3 128 bits RC4-SHA
     Accepted SSLv3 128 bits RC4-MD5
     Failed SSLv3 128 bits PSK-RC4-SHA
     Rejected SSLv3 56 bits EDH-RSA-DES-CBC-SHA
     Rejected SSLv3 56 bits EDH-DSS-DES-CBC-SHA
     Rejected SSLv3 56 bits ADH-DES-CBC-SHA
     Rejected SSLv3 56 bits DES-CBC-SHA
     Rejected SSLv3 40 bits EXP-EDH-RSA-DES-CBC-SHA
     Rejected SSLv3 40 bits EXP-EDH-DSS-DES-CBC-SHA
     Rejected SSLv3 40 bits EXP-ADH-DES-CBC-SHA
     Rejected SSLv3 40 bits EXP-DES-CBC-SHA
     Rejected SSLv3 40 bits EXP-RC2-CBC-MD5
     Rejected SSLv3 40 bits EXP-ADH-RC4-MD5
     Rejected SSLv3 40 bits EXP-RC4-MD5
     Rejected SSLv3 0 bits ECDHE-RSA-NULL-SHA
     Rejected SSLv3 0 bits ECDHE-ECDSA-NULL-SHA
     Rejected SSLv3 0 bits AECDH-NULL-SHA
     Rejected SSLv3 0 bits ECDH-RSA-NULL-SHA
     Rejected SSLv3 0 bits ECDH-ECDSA-NULL-SHA
     Failed SSLv3 0 bits NULL-SHA256
     Rejected SSLv3 0 bits NULL-SHA
     Rejected SSLv3 0 bits NULL-MD5
     Failed TLSv1 256 bits ECDHE-RSA-AES256-GCM-SHA384
     Failed TLSv1 256 bits ECDHE-ECDSA-AES256-GCM-SHA384
     Failed TLSv1 256 bits ECDHE-RSA-AES256-SHA384
     Failed TLSv1 256 bits ECDHE-ECDSA-AES256-SHA384
     Accepted TLSv1 256 bits ECDHE-RSA-AES256-SHA
     Rejected TLSv1 256 bits ECDHE-ECDSA-AES256-SHA
     Rejected TLSv1 256 bits SRP-DSS-AES-256-CBC-SHA
     Rejected TLSv1 256 bits SRP-RSA-AES-256-CBC-SHA
     Failed TLSv1 256 bits DHE-DSS-AES256-GCM-SHA384
     Failed TLSv1 256 bits DHE-RSA-AES256-GCM-SHA384
     Failed TLSv1 256 bits DHE-RSA-AES256-SHA256
     Failed TLSv1 256 bits DHE-DSS-AES256-SHA256
     Rejected TLSv1 256 bits DHE-RSA-AES256-SHA
     Rejected TLSv1 256 bits DHE-DSS-AES256-SHA
     Rejected TLSv1 256 bits DHE-RSA-CAMELLIA256-SHA
     Rejected TLSv1 256 bits DHE-DSS-CAMELLIA256-SHA
     Rejected TLSv1 256 bits AECDH-AES256-SHA
     Rejected TLSv1 256 bits SRP-AES-256-CBC-SHA
     Failed TLSv1 256 bits ADH-AES256-GCM-SHA384
     Failed TLSv1 256 bits ADH-AES256-SHA256
     Rejected TLSv1 256 bits ADH-AES256-SHA
     Rejected TLSv1 256 bits ADH-CAMELLIA256-SHA
     Failed TLSv1 256 bits ECDH-RSA-AES256-GCM-SHA384
     Failed TLSv1 256 bits ECDH-ECDSA-AES256-GCM-SHA384
     Failed TLSv1 256 bits ECDH-RSA-AES256-SHA384
     Failed TLSv1 256 bits ECDH-ECDSA-AES256-SHA384
     Rejected TLSv1 256 bits ECDH-RSA-AES256-SHA
     Rejected TLSv1 256 bits ECDH-ECDSA-AES256-SHA
     Failed TLSv1 256 bits AES256-GCM-SHA384
     Failed TLSv1 256 bits AES256-SHA256
     Accepted TLSv1 256 bits AES256-SHA
     Rejected TLSv1 256 bits CAMELLIA256-SHA
     Failed TLSv1 256 bits PSK-AES256-CBC-SHA
     Accepted TLSv1 168 bits ECDHE-RSA-DES-CBC3-SHA
     Rejected TLSv1 168 bits ECDHE-ECDSA-DES-CBC3-SHA
     Rejected TLSv1 168 bits SRP-DSS-3DES-EDE-CBC-SHA
     Rejected TLSv1 168 bits SRP-RSA-3DES-EDE-CBC-SHA
     Rejected TLSv1 168 bits EDH-RSA-DES-CBC3-SHA
     Rejected TLSv1 168 bits EDH-DSS-DES-CBC3-SHA
     Rejected TLSv1 168 bits AECDH-DES-CBC3-SHA
     Rejected TLSv1 168 bits SRP-3DES-EDE-CBC-SHA
     Rejected TLSv1 168 bits ADH-DES-CBC3-SHA
     Rejected TLSv1 168 bits ECDH-RSA-DES-CBC3-SHA
     Rejected TLSv1 168 bits ECDH-ECDSA-DES-CBC3-SHA
     Accepted TLSv1 168 bits DES-CBC3-SHA
     Failed TLSv1 168 bits PSK-3DES-EDE-CBC-SHA
     Failed TLSv1 128 bits ECDHE-RSA-AES128-GCM-SHA256
     Failed TLSv1 128 bits ECDHE-ECDSA-AES128-GCM-SHA256
     Failed TLSv1 128 bits ECDHE-RSA-AES128-SHA256
     Failed TLSv1 128 bits ECDHE-ECDSA-AES128-SHA256
     Accepted TLSv1 128 bits ECDHE-RSA-AES128-SHA
     Rejected TLSv1 128 bits ECDHE-ECDSA-AES128-SHA
     Rejected TLSv1 128 bits SRP-DSS-AES-128-CBC-SHA
     Rejected TLSv1 128 bits SRP-RSA-AES-128-CBC-SHA
     Failed TLSv1 128 bits DHE-DSS-AES128-GCM-SHA256
     Failed TLSv1 128 bits DHE-RSA-AES128-GCM-SHA256
     Failed TLSv1 128 bits DHE-RSA-AES128-SHA256
     Failed TLSv1 128 bits DHE-DSS-AES128-SHA256
     Rejected TLSv1 128 bits DHE-RSA-AES128-SHA
     Rejected TLSv1 128 bits DHE-DSS-AES128-SHA
     Rejected TLSv1 128 bits DHE-RSA-SEED-SHA
     Rejected TLSv1 128 bits DHE-DSS-SEED-SHA
     Rejected TLSv1 128 bits DHE-RSA-CAMELLIA128-SHA
     Rejected TLSv1 128 bits DHE-DSS-CAMELLIA128-SHA
     Rejected TLSv1 128 bits AECDH-AES128-SHA
     Rejected TLSv1 128 bits SRP-AES-128-CBC-SHA
     Failed TLSv1 128 bits ADH-AES128-GCM-SHA256
     Failed TLSv1 128 bits ADH-AES128-SHA256
     Rejected TLSv1 128 bits ADH-AES128-SHA
     Rejected TLSv1 128 bits ADH-SEED-SHA
     Rejected TLSv1 128 bits ADH-CAMELLIA128-SHA
     Failed TLSv1 128 bits ECDH-RSA-AES128-GCM-SHA256
     Failed TLSv1 128 bits ECDH-ECDSA-AES128-GCM-SHA256
     Failed TLSv1 128 bits ECDH-RSA-AES128-SHA256
     Failed TLSv1 128 bits ECDH-ECDSA-AES128-SHA256
     Rejected TLSv1 128 bits ECDH-RSA-AES128-SHA
     Rejected TLSv1 128 bits ECDH-ECDSA-AES128-SHA
     Failed TLSv1 128 bits AES128-GCM-SHA256
     Failed TLSv1 128 bits AES128-SHA256
     Accepted TLSv1 128 bits AES128-SHA
     Rejected TLSv1 128 bits SEED-SHA
     Rejected TLSv1 128 bits CAMELLIA128-SHA
     Failed TLSv1 128 bits PSK-AES128-CBC-SHA
     Accepted TLSv1 128 bits ECDHE-RSA-RC4-SHA
     Rejected TLSv1 128 bits ECDHE-ECDSA-RC4-SHA
     Rejected TLSv1 128 bits AECDH-RC4-SHA
     Rejected TLSv1 128 bits ADH-RC4-MD5
     Rejected TLSv1 128 bits ECDH-RSA-RC4-SHA
     Rejected TLSv1 128 bits ECDH-ECDSA-RC4-SHA
     Accepted TLSv1 128 bits RC4-SHA
     Accepted TLSv1 128 bits RC4-MD5
     Failed TLSv1 128 bits PSK-RC4-SHA
     Rejected TLSv1 56 bits EDH-RSA-DES-CBC-SHA
     Rejected TLSv1 56 bits EDH-DSS-DES-CBC-SHA
     Rejected TLSv1 56 bits ADH-DES-CBC-SHA
     Rejected TLSv1 56 bits DES-CBC-SHA
     Rejected TLSv1 40 bits EXP-EDH-RSA-DES-CBC-SHA
     Rejected TLSv1 40 bits EXP-EDH-DSS-DES-CBC-SHA
     Rejected TLSv1 40 bits EXP-ADH-DES-CBC-SHA
     Rejected TLSv1 40 bits EXP-DES-CBC-SHA
     Rejected TLSv1 40 bits EXP-RC2-CBC-MD5
     Rejected TLSv1 40 bits EXP-ADH-RC4-MD5
     Rejected TLSv1 40 bits EXP-RC4-MD5
     Rejected TLSv1 0 bits ECDHE-RSA-NULL-SHA
     Rejected TLSv1 0 bits ECDHE-ECDSA-NULL-SHA
     Rejected TLSv1 0 bits AECDH-NULL-SHA
     Rejected TLSv1 0 bits ECDH-RSA-NULL-SHA
     Rejected TLSv1 0 bits ECDH-ECDSA-NULL-SHA
     Failed TLSv1 0 bits NULL-SHA256
     Rejected TLSv1 0 bits NULL-SHA
     Rejected TLSv1 0 bits NULL-MD5
     Prefered Server Cipher(s):
     SSLv3 128 bits ECDHE-RSA-RC4-SHA
     TLSv1 128 bits ECDHE-RSA-RC4-SHA
    SSL Certificate:
     Version: 2
     [...]
     Signature Algorithm: sha1WithRSAEncryption
     Issuer: /C=ZA/O=Thawte Consulting (Pty) Ltd./CN=Thawte SGC CA
     Not valid before: Oct 26 00:00:00 2011 GMT
     Not valid after: Sep 30 23:59:59 2013 GMT
     [...]
     Public Key Algorithm: rsaEncryption
     RSA Public Key: (1024 bit)
     Public-Key: (1024 bit)
    [...]

```

Tem muita informação aí, não? Para que eu precisava tinha muita informação pois
o que era relevante saber era quais as versões de protocolo e os tipos de chave
criptográfica suportado pelo servidores web. Para o teste, usei a opção "**--no-failed**".

```
$ sslscan --no-failed www.site.com
     _
     ___ ___| |___ ___ __ _ _ __
     / __/ __| / __|/ __/ _` | '_ \
     \__ \__ \ \__ \ (_| (_| | | | |
     |___/___/_|___/\___\__,_|_| |_|




    Version 1.8.2
     http://www.titania.co.uk
     Copyright Ian Ventura-Whiting 2009




    Testing SSL server www.site.com on port 443




    Supported Server Cipher(s):
     Accepted SSLv3 256 bits ECDHE-RSA-AES256-SHA
     Accepted SSLv3 256 bits AES256-SHA
     Accepted SSLv3 168 bits ECDHE-RSA-DES-CBC3-SHA
     Accepted SSLv3 168 bits DES-CBC3-SHA
     Accepted SSLv3 128 bits ECDHE-RSA-AES128-SHA
     Accepted SSLv3 128 bits AES128-SHA
     Accepted SSLv3 128 bits ECDHE-RSA-RC4-SHA
     Accepted SSLv3 128 bits RC4-SHA
     Accepted SSLv3 128 bits RC4-MD5
     Accepted TLSv1 256 bits ECDHE-RSA-AES256-SHA
     Accepted TLSv1 256 bits AES256-SHA
     Accepted TLSv1 168 bits ECDHE-RSA-DES-CBC3-SHA
     Accepted TLSv1 168 bits DES-CBC3-SHA
     Accepted TLSv1 128 bits ECDHE-RSA-AES128-SHA
     Accepted TLSv1 128 bits AES128-SHA
     Accepted TLSv1 128 bits ECDHE-RSA-RC4-SHA
     Accepted TLSv1 128 bits RC4-SHA
     Accepted TLSv1 128 bits RC4-MD5




    Prefered Server Cipher(s):
     SSLv3 128 bits ECDHE-RSA-RC4-SHA
     TLSv1 128 bits ECDHE-RSA-RC4-SHA
    [...]
```


Também pode usar o [COMODO Site Analyzer](https://sslanalyzer.comodoca.com) para testar mas o servidor obrigatoriamente precisar estar disponível na internet.

Obs. Ah… Se você usa [Debian](http://www.debian.org) é bem simples de
instalar:

```
#aptitude install openssl sslscan
```
