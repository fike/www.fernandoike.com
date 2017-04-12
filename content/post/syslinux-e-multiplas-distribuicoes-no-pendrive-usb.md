+++
title = "Syslinux e multiplas distribuicoes no pendrive usb"
date = "2013-02-20"
draft = false
Categories = ["debian", "portugues", "SL"]
Tags = ["debian", "portugues", "syslinux", "boot", "linux"]
+++
Depois de alguns meses do [Ulisses (thebug)
Castro](http://www.ulissescastro.com) me atormentar para publicar, segue
um documento rápido para quem trabalha com muitas instalações de linux
em ambiente corporativo.

A instalação de distribuição linux usando CD ou DVD é um processo
relativamente rápido hoje. Se estiver fazendo a instalação em poucos
computadores é uma tarefa também tranquilo mas se estiver com um volume
grande de instalação e sua infra-estrutura de rede não estiver preparada
para instalação em massa de algumas centenas de servidores o processo de
instalação será manual e tedioso. Para alguns é um bem tedioso fazer
esse tipo de operação.

Uma das partes que realmente incomoda (ao menos para mim) é ter que
carregar algumas mídias de CD /DVD com alguns sabores de distribuições
Linux, então perguntando se era possível ter um pendrive USB (USB
flashdrive) que tivesse esses instaladores.

No vasto oceano de informações (internet) tem um excelente documento
escrito por [David
Heller](http://spirulina.wikispaces.com/file/view/Installing+Linux+from+a+USB+flashdrive.v20.pdf)
sobre instalação de [Red Hat](http://www.redhat.com) em USB flashdrive.
Porém é possível usar esse documento para qualquer outra distribuição, e
o programa chave para conseguir realizar a tarefa é o famoso
[Syslinux](http://www.syslinux.org).

No caso desta nota, foi preparado para duas distribuições:
[Debian](http://www.debian.org) e Red Hat (provavelmente funcionará no
[CentOS](http://www.centos.org) e [Fedora](http://fedoraproject.org/))
com seus respectivos instaladores. Presumindo que já tenha instalado o
syslinux via pacote iremos e tenha um pendrive disponível para uso .
Faça backup de seus dados, sem garantias de integridade de seus dados.

Supondo que o pendrive é reconhecido por seu linux como “/dev/sdb” e a
partição dele é reconhecida como “/dev/sdb1”. Segue:

1 - A imagem mbr está localizada em ”**/usr/lib/syslinux/**” e usaremos
o **dd** para copiar a imagem **mbr** para o pendrive.

    #dd if=/usr/lib/syslinux/mbr.bin of=/dev/sdb

2 - Após copiar o imagem mbr, copie o syslinux para o pendrive na
partição do mesmo.

    #syslinux /dev/sdb1

3 - Montar o pendrive em ”**/mnt/pendrive**”.

    #mount /dev/sdb1 /mnt/pendrive

4 - Copiar o **menu.c32**, localizado em ”**/usr/lib/syslinux**” para o
    pendrive.

    #cp /usr/lib/syslinux/menu.c32 /mnt/pendrive

5 - Criar os diretórios para os instaladores do Debian e Red Hat.

    #mkdir /mnt/pendrive/debian64
    #mkdir /mnt/pendrive/rh64

6 - Baixe o instalador do Debian para pendrive. Para esta nota, foi
    usado a versão do **Lenny** AMD64bits, também foi testado com o
    **Lenny** i386, **Etch** AMD64 e I386.

    #wget http://ftp.debian.org/debian/dists/lenny/main/installer-amd64/current/images/hd-media/boot.img.gz

7 - Descompactar a imagem do instalador Debian.

    #gunzip boot.img.gz

8 - Anexar (falta de nome mais apropriado) num dispositivo loopback para
ver o conteúdo da imagem.

    #losetup /dev/loop0 boot.img

9 - Mountar o dispositivo loopback com a imagem do instalador Debian.

    #mkdir /mnt /temp
    #mount -o loop /dev/loop0 /mnt/temp

10 - Copiar o kernel e a imagem initrd do Debian.

    #cp /mnt/temp/linux /mnt/pendrive/debian64
    #cp /mnt/temp/initrd.gz /mnt/pendrive/debian64

11 - Desmontar o ponto de montagem /mnt/temp.

    #umount /mnt/temp

12 - Liberar o dispositivo loopback usado para imagem Debian.

    #losetup -d /dev/loop0

No caso do Red Hat, será suposto para essa nota que já tenha a imagem do
mesmo. Os procedimentos funcionaram para a série 4.X e 5.X do Red Hat
Enterprise.

13 - Mountar a imagem de instalação do Red Hat, no caso aqui , usamos
uma imagem de DVD.

    #mount -o loop rhel-5.2-server-x86_64-dvd.iso /mnt/temp

14 - Copiar o kernel Red Hat e o initrd para o diretório
    ”**/mnt/pendrive/rh64**”

    #cp /mnt/temp/isolinux/vmlinuz /mnt/pendrive/rh64
    #cp /mnt/temp/isolinux/initrd.gz /mnt/pendrive/rh64

15 - Demontar a imagem do DVD Red Hat.

    #umount /mnt/temp

16 - Para ter um menu com opções ao iniciar um servidor/computador com o
pendrive com syslinux, precisará ter um menu com as opções de boot. O
syslinux buscará o arquivo syslinux.cfg, usando o seu editor favorito,
seguindo essa nota , ficará como abaixo:

    #vi /mnt/pendrive/syslinux.cfg
    DEFAULT menu.c32
    MENU TITLE Instalação Automatizada por pendrive
    LABEL Debian Lenny
    MENU LABEL Debian Lenny AMD 64 bits
    KERNEL debian64/linux
    APPEND linux initrd=debian64/initrd.gz priority=low vga= normal quiet –
    LABEL Red Hat 5 Update 2 AMD64
    MENU LABEL Red Hat 5 Update 2 AMD 64
    KERNEL rh64/vmlinuz
    APPEND linux load ramdisk= 1 initrd=rh64/initrd.img

O “MENU TITLE” pode escrever o que for mais conveniente. O “MENU LABEL”
é o descritivo de opção que aparecerá no momento do boot. O APPEND são
as opções para iniciar de cada instalação, no caso do Debian está
configurado para o debconf fazer todas as perguntas da instalação. Pode
mudar para o padrão das imagens de CD/DVD que é o médio alterando de
“priority=low” para “priority= medium”. Também é possível automatizar a
instalação do Debian e Redhat usando os recursos de **Seed** (Debian) ou
o **Kickstart** (Red Hat) mas isso ficar para outra nota.

17 - Por fim, copiar as imagens de instalação (Debian e Red Hat) para
”**/mnt/pendrive**”. Lembre-se que o tamanho do pendrive pode limitar a
quantidade de imagens que pode usar ao mesmo tempo, como uso um pendrive
de 4GB, foi copiado a instalação do Debian Lenny via Rede (netinstall) e
o DVD completo da instalação do Red Hat 5.2.

    #cp debian-testing-amd64-netinst.iso /mnt/pendrive
    #cp rhel-5.2-server-x86_64-dvd.iso /mnt/pendrive

18 - O fim com uma imagem de um exemplo de um pendrive preparado para
múltiplos instaladores Linux. Outras distribuições Linux também permitem
este tipo de instalação, teste aí e avise .

![](/images/syslinux.png)

    dd if=/ sr/lib/syslinux/mbr.bin of= /dev/sdb

    syslinux /dev/sdb1
    mount /dev/sdb1 /mnt/pendrive

    cp /usr/lib/syslinux/menu.c32 /mnt/pendrive
    mkdir /mnt/pendrive/debian64
    mkdir /mnt/pendrive/rh64

    wget http://ftp.debian.org/debian/dists/lenny/main/installer-amd64/current/images/hd-media/boot.img.gz

    gunzip boot.img.gz
    losetup /dev/loop0 boot.img
    mkdir /mnt /temp
    mount -o loop /dev/loop0 /mnt/temp
    cp /mnt/temp/linux /mnt/pendrive/debian64
    cp /mnt/temp/initrd.gz /mnt/pendrive/debian64

    umount /mnt/temp
    losetup -d /dev/loop0

    cat /mnt/pendrive/syslinux.cfg
    DEFAULT menu.c32
    MENU TITLE Instalação Automatizada por pendrive
    LABEL Debian Lenny
    MENU LABEL Debian Lenny AMD 64 bits
    KERNEL debian64/linux
    APPEND linux initrd=debian64/initrd.gz priority=low vga= normal quiet –
    LABEL Red Hat 5 Update 2 AMD64
    MENU LABEL Red Hat 5 Update 2 AMD 64
    KERNEL rh64/vmlinuz
    APPEND linux load _ramdisk= 1 initrd=rh64/initrd.img

    cp debian-testing -amd64- netinst. iso /mnt/pendrive
    cp rhel-5 .2- server-x 86_64-dvd .iso /mnt/pendrive

    dd if=/usr/lib/syslinux/mbr.bin of=/dev/sdb

    syslinux /dev/sdb1
    mount /dev/sdb1 /mnt/pendrive

    cp /usr/lib/syslinux/menu.c32 /mnt/pendrive
    mkdir /mnt/pendrive/debian64
    mkdir /mnt/pendrive/rh64

    mount -o loop rhel-5.2-server-x86_64-dvd.iso /mnt/temp

    gunzip boot.img .gz
    losetup /dev/loop0 boot.img
    mkdir /mnt /temp
    mount -o loop /dev/loop0 /mnt/temp
    cp /mnt/temp/isolinux/vmlinuz /mnt/pendrive/rh64
    cp /mnt/temp/isolinux/initrd.gz /mnt/pendrive/rh64

    umount /mnt/temp
    losetup -d /dev/loop0

    cat /mnt /pendrive/syslinux.cfg

    cp debian-testing -amd64- netinst. iso / mnt/ pendrive
    cp rhel-5 .2- server-x 86_64-dvd .iso /mnt /pendrive
