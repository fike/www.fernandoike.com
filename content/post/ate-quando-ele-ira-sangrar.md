+++
title = "Ate quando ele ira sangrar"
date = "2014-04-18"
draft = false
Categories = ["portugues", "debian", "SL"]
Tags = ["portugues", "debian", "openssl", "heartbleed", "TLS"]
+++
Até quando corações irão sangrar?

![]( /images/heartbleed.png)

Refazendo a pergunta, até quando teremos novidades sobre as falhas do
[OpenSSL](https://www.openssl.org/) e o Heartbleed? Hoje, talvez, seja a
pergunta de um milhão de obamas.

Você, querido (e raro) leitor deve ter visto em milhares de sites o
transtorno que o [HeartBleed](http://heartbleed.org) está causando. Pelo
impacto causado é provável que seja a maior falha de segurança na era da
Internet 2.0.

Resumindo o que pude compilar:

[Robin Seggelmann](http://www.robin-seggelmann.de/) enviou um
[patch](http://rt.openssl.org/Ticket/Display.html?id=2658&user=guest&pass=guest)
para o OpenSSL implementando a extensão Heartbeat para TLS (RFC
6520)[8](https://tools.ietf.org/html/rfc6520). Infelizmente com ela foi
também entrou a falha que permite capturar as chaves privadas, essa
falha foi chamada pelo [Codenomicon](http://www.codenomicon.com/) como
HeartBleed.

O xkcd fez um [quadrinho](http://xkcd.com/1354/) interessante sobre a
falha.

[![](/images/heartbleed_explanation.png "XKCD")](http://imgs.xkcd.com/comics/heartbleed_explanation.png)

O bom texto para entender um pouco mais o bug, é ir ao
[IDGNow](http://idgnow.com.br/internet/2014/04/10/heartbleed-conheca-ameaca-que-atingiu-a-internet-e-veja-como-se-proteger/).

O patch foi enviado pelo Robin Seggelmann em Dezembro de 2011 e entrou
na versão 1.0.1 (Abril de 2012), afetando as versões posteriores até a
**1.0.1f**. Algumas formas de contornar são atualizar para versão
**1.0.1g** ou compilar novamente o Openssl usando a flag
**-DOPENSSL\_NO\_HEARTBEATS**. Se você estiver usando servidor web
(Apache, Nginx, etc) e usar SSL para HTTPS, considere gerar novamente os
certificados, nos meus testes usando certificado com certificado antigo
e o OpenSSL atualizado continuo apresentando problema com Heartbleed.

O impacto é tão significativo que praticamente todos os grandes serviços
na internet bloquearam as senhas antigas forçando os usuários gerarem
novamente. Na semana passada tinha até [uma
lista](https://gist.github.com/dberkholz/10169691/) no Github com os
sites mais famosos que ainda não tinha atualizado o OpenSSL e os
[certificados](http://idgnow.com.br/internet/2014/04/10/heartbleed-conheca-ameaca-que-atingiu-a-internet-e-veja-como-se-proteger/).

Além dos servidores web, outros softwares foram afetados?

Provavelmente sim, ao menos na teoria, todos os softwares que usam TLS
estão potencialmente estão vulneráveis. O
[OpenSSH](http://www.openssh.com/) não foi afetado em princípio (até que
alguém provar que sim…), outros serviços que usam somente SSLv3 também
não. Entretanto, comenta-se que o [Android na versão
4.1.1](http://mashable.com/2014/04/11/devices-running-android-4-1-1-vulnerable-to-heartbleed/)
tem o Hearbleed e todos os dispositivos que usam o [BlackBerry
Messenger](http://www.ctvnews.ca/sci-tech/heartbleed-poses-bbm-risk-on-apple-android-devices-blackberry-warns-1.1775020)
também foram comprometidos. Não posso deixar de mencionar que também foi
[anunciado](http://www.networkworld.com/news/2014/041014-heartbleed-cisco-juniper-280593.html)
que alguns equipamentos da Cisco e Juniper entraram na lista também. A
Oracle
[listou](http://www.oracle.com/technetwork/topics/security/opensslheartbleedcve-2014-0160-2188454.html)
quais versões de seus produtos foram afetados pelo bug.

Em meio a tempestade a Akamai enviou um [patch
inicial](http://www.cnet.com/news/akamai-heartbleed-patch-not-a-fix-after-all/)
para o OpenSSL com a intenção de melhorar a segurança no armazenamento
das chaves privadas do SSL, entretanto [Willem
Pinckaers](http://lekkertech.net) questionou a efetividade do patch.
Provável que tenha novas revisões evolutivas do patch até que seja
incorporado em defitinitivo no OpenSSL.

Considerando que o Heartbleed está nos servidores web desde 2012, o
quanto as senhas e dados de milhões de usuários foram vazados. É
impossível contabilizar porque são dois anos em que a falha esteve
disponível sem nenhum alarde.

As recomendações no geral são: atualizar o OpenSSL, gerar novamente as
chaves privadas e trocar as senhas. Recomendo que daqui um tempo, troque
novamente as senhas porque o Hearbleed porque ainda tem muita coisa pela
frente. Pelo que a Bloomblerg
[noticiou](http://www.bbc.com/news/technology-27058143), a NSA sabia da
existência do bug há dois anos. Quem mais sabia? Provavelmente muitos
outros, infezlimente.

O Pessoal do Elastica criou um [vídeo](http://vimeo.com/91425662)
explicando como é o HeartBleed.
[![](/images/heartbleed_elastica.jpg "Elastica Video")](http://vimeo.com/91425662)

Isso me lembrou uma outra
[falha](http://www.debian.org/security/2008/dsa-1571) que causou um
grande alvoroço e que acidentalmente foi introduzida também no OpenSSL
(0.9.8c-1) mas especificamente no Debian e derivados. A falha foi
descoberta em Maio de 2008 pelo [Luciano
Bello](http://www.lucianobello.com.ar/) e ela comprometeu as chaves SSH,
OpenVPN e DNSSEC.

O curioso que até os produtos e os serviços da Microsoft e outras
empresas com a cultura de software proprietários não foram afetados e
tem muitos “especialistas” alegando que os produtos/sistemas deles são
mais seguros. Esse argumento é levemente falso porque o Heartbleed
somente teve essa repercussão grande porque o OpenSSL tem uma licença
considerada Código Aberto (“Software Livre”). Se o OpenSSL tivesse uma
licença como a maioria dos produtos da Microsoft, provavelmente não
saberíamos que ele existia.

Algumas pessoas são bem críticas ao OpenSSL, principalmente pela código
enorme (200 mil linhas) e de qualidade duvidosa. Ao menos é o que diz o
[Poul-Henning Kamp](http://phk.freebsd.dk/), desenvolvedor e Varnish.
Recomendo ler [o artigo](http://queue.acm.org/detail.cfm?id=2602816)
(inglês) na [ACM].

Alternativas?

[GnuTLS](http://www.gnutls.org/) e [PolarSSL](https://polarssl.org/) são
algumas. Se alguém já usou algum em seus projetos, conte a experiência
para nós. :)

O pessoal do OpenBSD fez um fork ([LibreSSL](http://www.libressl.org/))
e estão fazendo uma pequena faxina no código para que falhas como o
Heartbleed tenha pouca probabilidade de acontecer.

O [artigo na Wikipedia](http://en.wikipedia.org/wiki/Heartbleed) do
Heartbleed é a melhor compilação sobre o bug. Vale a leitura.
