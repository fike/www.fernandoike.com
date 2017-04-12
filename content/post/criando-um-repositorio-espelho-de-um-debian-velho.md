+++
title = "Criando um repositorio espelho de um Debian velho"
date = "2013-01-07"
draft = false
Categories = ["debian", "SL", "portugues"]
Tags = ["portugues", "debian", "SL", "debmirror", "lenny"]
+++
Lembra que eu tive que[instalar uma versão antiga](http://www.fernandoike.com/2012/12/27/instalando-um-debian-velho-lenny/) do
Debian e tive [um probleminha para instalar pacotes](http://www.fernandoike.com/2012/12/28/timeout-para-instalar-pacotes-no-debian-velho/) dele?

Pois é, a saga continua…

Tive que criar também um espelho do repositório Lenny para manter numa
rede fechada (sem internet) e para criar usei o debmirror. Não me
preocupei em criar um script com tratamento já que está versão do Debian
não tem mais nenhum tipo de atualização.

    debmirror --nosource --host=archive.debian.org --method=http \
     --rsync-extra=none --dist=lenny --arch=amd64 \
    --section=main,contrib,non-free --cleanup --ignore-release-gpg \
    --progress --verbose /srv/mirror/debian

Uma das formas de configurar o novo repositório é como está abaixo:

    echo "deb file:///opt/debian/ lenny main non-free contrib" >> /etc/apt/sources.list

Obs.: Destacando, nunca use esta ou qualquer outra versão sem suporte
oficial em ambiente de produção. ;)
