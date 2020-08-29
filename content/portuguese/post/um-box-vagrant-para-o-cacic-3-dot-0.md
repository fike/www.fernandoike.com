+++
title = "Um box vagrant para o cacic 3 dot 0"
date = "2013-10-08"
draft = false
categories = ["SL", "portugues", "debian"]
tags = ["vagrant", "SL", "cacic", "portugues"]
+++
Se quiser ajudar no desenvolvimento ou teste, pode usar um box vagrant
que criei com a versão **3.0** beta que está disponibilizado no [Portal
do Software Público](https://www.softwarepublico.gov.br/).

O [Vagrant](https://www.vagrantup.com/) permite criar ambientes de
desenvolvimento, teste, etc. muito facilmente e sem precisar usar a
interface gráfica do [virtualbox](https://www.virtualbox.org/) para
isso. Lembrando que a VM criada pelo template nunca deve ser usado em
produção, até porque ela não tem grandes recursos configurados. Mas pode
usar alguma coisa como [chef](https://www.opscode.com/chef/),
[puppet](https://puppetlabs.com/), etc. para envir para um ambiente de
produção do jeito certo. ;)

Vagrant está disponível para várias distribuições linux, no
[Debian](https://www.debian.org/) é bem fácil porque já tem no
repositório oficial. No site do Vagrant tem
[pacotes](https://downloads.vagrantup.com/tags/v1.3.4) para instalar para
diferentes sistemas operacionais e distribuições linux, pode dar uma
olhada lá.

Depois de instalado e baixado o arquivo box
([cacic-server-3.0b.box](https://www.softwarepublico.gov.br/dotlrn/clubs/cacic/forums/message-view?message_id=78489902)),
os passos seguintes são bem simples.

```
$vagrant box add base cacic-server-3.0b.box

$vagrant init

$vagrant up

$vagrant ssh
```

Estes box está configurado com uma segunda placa de rede em modo bridge,
então pode usá-la para que vm fique disponível na rede.

A instalação está exatamente como a documentação cita: diretórios do
cacic, serviços, pacotes, etc. Exceto por duas coisas diferentes.

1 - Ao invés de editar o php.ini para alterar o fuso horário do
[PHP](https://www.php.net), incluí um arquivo

```
$cat /etc/php5/apache2/conf.d/30-timezone.ini
date.timezone = America/Sao_Paulo
```

2 - Ao invés do [Proftpd](https://www.proftpd.org/), usei o
[Vsftpd](https://vsftpd.beasts.org/). Ele é mais simples de usar.

Para acessar, basta usar o *IP* da *eth1* que você configurar.
https://ip-servidor/cacic/app.php

Obs. Esse VM é Debian Wheezy 7.0 AMD64 (64 bits)
