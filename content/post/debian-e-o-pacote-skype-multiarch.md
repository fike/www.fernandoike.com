+++
title = "Debian e o pacote skype multiarch"
date = "2013-03-29"
draft = false
Categories = ["debian", "portugues", "skype", "SL"]
Tags = ["portugues", "debian", "multiarch", "skype"]
+++
Estive que reinstalar meu computador e por causa do trabalho tive que
instalar o [Skype](http://www.skype.com). Já tem muito tempo que o
computador de uso cotidiano roda um Sistema Operacional [64
bits(AMD64/x86-64)](http://en.wikipedia.org/wiki/X86-64), e dessa vez
não foi diferente. Uma única coisa que mudou um pouquinho da última
instalada é o pacote multi arquitetura do Skype.

Aliás, isso é uma das grandes novidades (Leia a [Nota de
Lançamento](http://www.debian.org/releases/wheezy/releasenotes)) do
Debian para a próxima versão estável do [Debian](http://www.debian.org)
que deve sair nos próximos dias (espero!).

Bom, não é tão complicada porque uma versão instalada do Debian possui
suporte a multi arquitetura ([multiarch][]) mas também não é tão simples
como instalar um pacote.

Se for tentar instalar o pacote do Skype diretamente com o **dpkg**,
provavelmente terá o retorno do comando parecido com o que está logo
abaixo.

```
root@klatoon:~# dpkg -i /home/fike/Downloads/skype-debian_4.1.0.20-1_i386.deb
dpkg: error processing /home/fike/Downloads/skype-debian_4.1.0.20-1_i386.deb (--install):
 package architecture (i386) does not match system (amd64)
Errors were encountered while processing:
 /home/fike/Downloads/skype-debian_4.1.0.20-1_i386.deb
```

Isso acontece porque o **Sistema Operacional** ainda não está preparado
para suportar mais de uma arquitetura, para acrescentar basta adicionar
usando o **dpkg**.

```
dpkg --add-architecture i386
```

E você provavelmente sabia apenas que o **dpkg** instala e desinstala
pacote, hein? Felizmente ele faz muito mais coisa. ;)

Adicionado mais uma arquitetura, agora é necessário modificar um
pouquinho o repositório de pacotes. Normalmente o **sources.list** é
parecido como este abaixo:

```
deb [arch=amd64,i386] http://ftp.br.debian.org/debian/ sid main non-free contrib
```

Para ter acesso ao repositório da arquitetura adicionada é necessário
deixar explícito no sources.list.

```
editor /etc/apt/source.list
deb [arch=amd64,i386] http://ftp.br.debian.org/debian/ sid main non-free contrib
```

Acrescentado o novo repositório, é necessário atualizar o aptitude.

```
aptitude update
```

Antes de empolgar-nos para ter o Skype já funcionando é necessário mais
alguns passo ou senão pode acontecer um erro como o abaixo

```
dpkg -i /home/fike/Downloads/skype-debian_4.1.0.20-1_i386.deb
Selecting previously unselected package skype.
(Reading database ... 176029 files and directories currently installed.)
Unpacking skype (from .../skype-debian_4.1.0.20-1_i386.deb) ...
dpkg: dependency problems prevent configuration of skype:
 skype depends on libasound2 (>= 1.0.16); however:
  Package libasound2 is not installed.
 skype depends on libc6 (>= 2.3.6-6~); however:
  Package libc6 is not installed.
 skype depends on libc6 (>= 2.7); however:
  Package libc6 is not installed.
 skype depends on libgcc1 (>= 1:4.1.1); however:
  Package libgcc1 is not installed.
 skype depends on libqt4-dbus (>= 4:4.5.3); however:
  Package libqt4-dbus is not installed.
 skype depends on libqt4-network (>= 4:4.8.0); however:
  Package libqt4-network is not installed.
 skype depends on libqt4-xml (>= 4:4.5.3); however:
  Package libqt4-xml is not installed.
 skype depends on libqtcore4 (>= 4:4.7.0~beta1); however:
  Package libqtcore4 is not installed.
 skype depends on libqtgui4 (>= 4:4.8.0); however:
  Package libqtgui4 is not installed.
 skype depends on libqtwebkit4 (>= 2.1.0~2011week13); however:
  Package libqtwebkit4 is not installed.
 skype depends on libstdc++6 (>= 4.6); however:
  Package libstd
dpkg: error processing skype (--install):
 dependency problems - leaving unconfigured
Processing triggers for gnome-menus ...
Processing triggers for desktop-file-utils ...
Errors were encountered while processing:
 skype
```

Veja que os erros acima são de dependências mas nem pense em usar o
aptitude para resolver as dependências para instalar o Skype porque
provavelmente irá ter um probleminha ao usar fazê-lo.

```
root@klatoon:~# aptitude -f install
The following partially installed packages will be configured:
  skype:i386{b}
No packages will be installed, upgraded, or removed.
0 packages upgraded, 0 newly installed, 0 to remove and 2 not upgraded.
Need to get 0 B of archives. After unpacking 0 B will be used.
The following packages have unmet dependencies:
 skype:i386 : Depends: libasound2:i386 (>= 1.0.16) but it is not going to be installed.
              Depends: libc6:i386 (>= 2.3.6-6~) but it is not going to be installed.
              Depends: libc6:i386 (>= 2.7) but it is not going to be installed.
              Depends: libgcc1:i386 (>= 1:4.1.1) but it is not going to be installed.
              Depends: libqt4-dbus:i386 (>= 4:4.5.3) but it is not going to be installed.
              Depends: libqt4-network:i386 (>= 4:4.8.0) but it is not going to be installed.
              Depends: libqt4-xml:i386 (>= 4:4.5.3) but it is not going to be installed.
              Depends: libqtcore4:i386 (>= 4:4.7.0~beta1) but it is not going to be installed.
              Depends: libqtgui4:i386 (>= 4:4.8.0) but it is not going to be installed.
              Depends: libqtwebkit4:i386 (>= 2.1.0~2011week13) but it is not going to be installed.
              Depends: libstdc++6:i386 (>= 4.6) but it is not going to be installed.
              Depends: libx11-6:i386 but it is not going to be installed.
              Depends: libxext6:i386 but it is not going to be installed.
              Depends: libxss1:i386 but it is not going to be installed.
              Depends: libxv1:i386 but it is not going to be installed.
              Depends: libssl1.0.0:i386 but it is not going to be installed.
The following actions will resolve these dependencies:

     Remove the following packages:
1)     skype:i386



Accept this solution? [Y/n/q/?]
```


A alternativa para esta situação é instalar manualmente as dependências.

```
aptitude install gcc-4.7-base:i386 libasound2:i386 libaudio2:i386 \
  libavahi-client3:i386 libavahi-common-data:i386 libavahi-common3:i386  \
  libc6:i386 libc6-i686:i386  libcomerr2:i386 libcups2:i386 \
  libdbus-1-3:i386 libexpat1:i386  libffi5:i386 libfontconfig1:i386  \
  libfreetype6:i386 libgcc1:i386 libgcrypt11:i386 libglib2.0-0:i386  \
  libgnutls26:i386 libgpg-error0:i386 libgssapi-krb5-2:i386 \
  libgstreamer-plugins-base0.10-0:i386 libgstreamer0.10-0:i386 libice6:i386  \
  libjbig0:i386 libjpeg8:i386 libk5crypto3:i386 libkeyutils1:i386 \
  libkrb5-3:i386 libkrb5support0:i386 liblcms1:i386 liblzma5:i386 \
  libmng1:i386 liborc-0.4-0:i386 libp11-kit0:i386 libpcre3:i386 \
  libpng12-0:i386 libqt4-dbus:i386 libqt4-network:i386 libqt4-xml:i386 \
  libqtcore4:i386 libqtdbus4:i386 libqtgui4:i386 libqtwebkit4:i386 \
  libselinux1:i386 libsm6:i386 libsqlite3-0:i386 libstdc++6:i386 \
  libtasn1-3:i386 libtiff4:i386 libuuid1:i386 libx11-6:i386 libxau6:i386 \
  libxcb1:i386 libxdmcp6:i386 libxext6:i386  libxml2:i386 libxrender1:i386 \
  libxt6:i386  zlib1g:i386 libxss1:i386 libxv1:i386 libssl1.0.0:i386 \
  libasound2-plugins:i386
```

Se por alguma razão o pacote do Skype foi desinstalado na instalação das
dependências, só executar novamente.

```
root@klatoon:~# dpkg -i /home/fike/Downloads/skype-debian_4.1.0.20-1_i386.deb
```
