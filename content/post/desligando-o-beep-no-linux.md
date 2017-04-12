+++
title = "Desligando o beep no linux"
date = "2013-04-08"
draft = false
Categories = ["debian", "portugues", "SL"]
Tags = ["portugues", "linux", "audio"]
+++
Minha memória bugada precisa deste texto. :)

Uso muito linux em modo texto, seja num terminal gráfico ou numa sessão
mesmo.

Geralmente eu reinstalo o Sistema Operacional do meu computador para
testar alguns instaladores de distribuiçao linux, etc. Porém eu sempre
esqueço de de desligar o maldito bipe que o terminal emite ao apertar a
tecla TAB. Então fica o registro para minha memória.

Para resolver esse problema é necessário criar uma entrada para bloquear
o carregamento do módulo *pcspkr*.

    # echo "blacklist pcspkr" > /etc/modprobe.d/custom.conf

Ou se o bipe está incomodando agora e quer parar agora:

    # rmmod pcspkr
