+++
title = "Videoconf do hangout caindo no Debian"
date = "2014-01-14"
draft = false
Categories = ["portugues", "SL", "debian"]
Tags = ["portugues", "hangout", "debian", "videoconferencia"]
+++
Ultimamente tenho participado de muitas reuniões por videoconferência
usando o [Skype](http://skype.com) ou
[Hangout](http://www.google.com/+/learnmore/hangouts/?hl=pt-BR). O
Hangout especificamente não estava funcionando direito no meu
[Debian](http://www.debian.org)
[Sid](http://www.debian.org/releases/sid/), ao iniciar a
videoconferência, ela caía automaticamente.

Procurando um pouco encontrei no [fórum de
produto](http://productforums.google.com/forum/#!topic/hangouts/vYsaeEnXJXs)
do Hangout pessoas com problema similar e que resolveram removendo o
pacote **libudev0**.


```
#aptitude remove libudev0
```
