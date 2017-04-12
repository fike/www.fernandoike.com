+++
title = "Usando a ultima versao do firefox no debian"
date = "2013-04-03"
draft = false
Categories = ["web", "debian", "firefox", "portugues", "SL"]
Tags = ["web", "debian", "portugues", "firefox", "iceweasel"]
+++
![](/images/iceweasel.png)

Se você é usuário [Debian](http://www.debian.org), provavelmente usa o
[Iceweasel](http://www.geticeweasel.org/). Iceweasel é o
[Firefox](http://www.mozilla.org/pt-BR/firefox/new/) sem a restrição de
marca imposta pela [Fundação Mozilla](http://www.mozilla.org) e backport
dos patchs de segurança para a versão estável do Debian.

Como no momento novas versões de pacotes estão congeladas por causa do
que a próxima versão estável do Debian está para ser lançada em breve, a
versão corrente tanto no [Sid](http://www.debian.org/releases/sid/) como
no [Wheezy](http://www.debian.org/releases/wheezy/) é a **10.0**. Isso
não chega ser um problemas para a maioria dos usuários mas para mim é
porque no meu trabalho tenho que testar as últimas versões dos
navegadores.

Se você precisa da versão mais nova do Firefox e quer instalar na forma
“Debian Way” pode fazer facilmente.

Acrescente o respositório
[experimental](http://wiki.debian.org/DebianExperimental) no
sources.list e atualize com teu gerenciador de pacotes favorito. No meu
caso é o aptitude

```
#echo "deb http://ftp.br.debian.org/debian/ experimental main non-free contrib" >> /etc/apt/sources.list
#aptitude update
```


Normalmente nenhum pacote da experimental é instalado por padrão, exceto
quando ele é explicitamente declarado, então para o aptitude é como está
abaixo.

```
#aptitude -t experimental install iceweasel iceweasel-l10n-ptbr
```

Lembrando que no momento a versão na experimental é 20.0. Se precisar
ver como instalar versões mais novas do Firefox, visite o do [Time de
Empacomento Mozilla](http://mozilla.debian.net/)
