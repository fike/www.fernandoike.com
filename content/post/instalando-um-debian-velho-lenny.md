+++
title = "Instalando um Debian velho lenny"
date = "2012-12-27"
draft = false
Categories = ["debian", "SL", "portugues"]
Tags = ["portugues", "debian", "lenny", "oldstable"]
+++
![](/images/debian-lenny.jpg)

Não pergunte porque eu tive usar uma versão bem antiga do
[Debian](http://www.debian.org)! Tem coisas que você apenas precisa
saber que existem… ;)

Se por alguma razão muito pouco comum você precisa instalar uma versão
antiga do Debian, como eu que tive que instalar um
[Lenny](http://www.debian.org/releases/lenny) (versão 5.0.x e lançado em
2009) para um serviço muito específico do trabalho. Caso não saiba, o
Lenny deixou de ser “suportado” oficialmente esse ano de 2012,
entenda-se “suportado” como atualizar os pacotes da versão em caso de
uma falha de segurança, bug crítico, etc.

Voltando a instalação, para baixar a instalador do Lenny, você pode
baixar uma cópia
[aqui](http://www.debian.org/releases/lenny/debian-installer/). A
instalação não tem muito segredo, apenas ter o cuidado no momento de
adicionar o repositório que usará para baixar os pacotes. No source.list
terá uma linha parecida com abaixo:

    deb http://archive.debian.org/debian/ lenny main

Remova a linha que contém o repositório de segurança, afinal para o
Lenny não tem mais suporte.

    deb http://security.debian.org/ lenny/updates main

Ainda curioso porque tive que instalar o Lenny;? Quem sabe num gnubeer
qualquer eu conto. :P
