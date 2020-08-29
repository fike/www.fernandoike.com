+++
title = "Videoconf do hangout caindo no Debian"
date = "2014-01-14"
draft = false
categories = ["portugues", "SL", "debian"]
tags = ["portugues", "hangout", "debian", "videoconferencia"]
+++
Ultimamente tenho participado de muitas reuniões por videoconferência
usando o [Skype](https://skype.com) ou
[Hangout](https://www.google.com/+/learnmore/hangouts/?hl=pt-BR). O
Hangout especificamente não estava funcionando direito no meu
[Debian](https://www.debian.org)
[Sid](https://www.debian.org/releases/sid/), ao iniciar a
videoconferência, ela caía automaticamente.

Procurando um pouco encontrei no [fórum de
produto](https://productforums.google.com/forum/#!topic/hangouts/vYsaeEnXJXs)
do Hangout pessoas com problema similar e que resolveram removendo o
pacote **libudev0**.


```
#aptitude remove libudev0
```
