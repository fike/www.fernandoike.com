+++
title = "Skype e computadores com duas placas de video"
date = "2013-12-16"
draft = false
Categories = ["portugues", "debian", "SL"]
Tags = ["portugues", "debian", "skype", "nvidia", "bumblebee"]
+++
Infelizmente uso muito [Skype](http://www.skype.com) no trabalho e
estava com um problema com ele ao participar de videoconferências, ele
simplesmente caia (famoso **segment fault**). Depois de um tempo ele
automagicamente voltou a funcionar.

Conversando com o [Euler](http://eulerto.blogspot.com.br/) e tentando
ajudá-lo a fazer o Skype funcionar, percebi que esse problema acontece
em computadores que tem duas placa de vídeos e os drivers do kernel
[linux](https://wiki.debian.org/Bumblebee) estão carregados na memória.
Se você está com um problema como esse e tem duas placas de vídeo (no
meu caso, a segunda placa é uma Nvidia), pode usar o
[bumblebee](http://bumblebee-project.org/) para contornar o problema.

O projeto Bumblebee permite usar a tecnologia [Nvidia
Optimus](http://www.nvidia.com.br/object/optimus_technology_br.html). O
principal ganho em instalar o bumblebee é melhorar o gerenciamento de
energia e ganhar alguns minutos a mais ao usar a bateria do notebook.

Para instalá-lo no [Debian](http://www.debian.org) é relativamente
simples, basta:

```
#aptitude bumblebee
```

Se quiser executar o Skype pela placa de vídeo Nvidia:

```
$optirun skype
```
