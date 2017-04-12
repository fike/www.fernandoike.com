+++
title = "Banco do brasil e openjdk"
date = "2014-09-03"
draft = false
Categories = ["debian", "SL", "portugues", "java", "SL"]
Tags = ["portugues", "banco do brasil", "java", "openjdk", "icedtea", "plugin", "debian"]
+++
Banco do Brasil e OpenJDK

Para usar o internet banking do Banco do Brasil num [Debian][debian] 64 bits
era um pouco mais trabalhoso do que outros sistemas operacionais. Para
usá-lo, eu tinha uma máquina virtual ([Virtualbox][virtualbox]) 32 bits
com Debian [Wheezy][wheezy] instalado e o
[OpenJDK][openjdk]+[Icedtea][icedtea].

Poderia usar a JVM da Oracle? Sim, poderia mas é mais trabalhoso manter
ela atualizada do que usar uma máquina virtual 32 bits.

Algum tempo atrás, o *ricardoperera* perguntou no canal de IRC do Debian
Brasil (sim, ainda uso IRC...) se alguém tinha dica de como acessar o
internet banking usando o Wheezy. Minha sugestão para ele foi usar uma vm
em 32 bits e passei o [template][link_template] do [Veewee][veewee] para instalar tudo que precisa
para acessar o internet banking.

O tiago_tm sugeriu uma abordagem melhor, usar o **setarch**.

```
fike@klatoon:/tmp$ setarch x86_64 --uname-2.6 iceweasel
```


[virtualbox]: https://www.virtualbox.org/
[openjdk]: http://openjdk.java.net/
[icedtea]: http://icedtea.classpath.org/
[wheezy]: https://www.debian.org/releases/wheezy
[debian]: http://www.debian.org
[veewee]: https://github.com/jedi4ever/veewee
[link_template]: https://github.com/fike/veewee-definitions/tree/master/debgui32
