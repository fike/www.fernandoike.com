+++
title = "Pbuilder e pdebuilder"
date = "2013-09-13"
draft = false
Categories = ["SL", "debian", "portugues"]
Tags = ["portugues", "SL", "debian", "pbuilder"]
+++
Criar pacotes deb (do jeito certo) é trabalhoso. Depois que pega o jeito
é bem mais fácil mas ainda sim trabalhoso, principalmente quando é
necessário fazer algum teste. Uma das formas de automatizar isso é usar
o
[pbuilder](http://www.netfort.gr.jp/~dancer/software/pbuilder-doc/pbuilder-doc.html).
Ele permite gerar pacotes usando uma ambientes de jaula (chroot) e gerar
pacotes para diferentes versões do [Debian](http://www.debian.org),
([Ubuntu](http://www.ubuntu.com)) e outros. Por exemplo, criando alguns
ambientes chroot com versões diferentes de Linux (GNU/Linux) e
arquitetura de hardware.

Criando os ambientes chroots
----------------------------

Debian Sid/Unstable em AMD64
```
$sudo pbuilder create --basetgz /var/cache/pbuilder/base-sid-amd64.tgz \
      --distribution sid
```

Debian Wheezy (Stable) em I386 (ia32)
```
$pbuilder create --basetgz /var/cache/pbuilder/base-stable-i386.tgz \
      --distribution stable --architecture i386
```

Caso esteja usando Debian e queirar gerar um pacote para Ubuntu. Pode
fazer também mas terá que adicionar a chave pública do Ubuntu no apt
antes de criar. No exemplo abaixo é o Ubuntu Raring Ringtail (13.04).
```
$sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 3B4FE6ACC0B21F32

$sudo pbuilder create --basetgz /var/cache/pbuilder/base-raring-amd64.tgz \
      --distribution raring --mirror http://ftp.ubuntu.com/ubuntu \
      --debootstrapopts --keyring=/etc/apt/trusted.gpg
```

Gerando os pacotes
------------------

### pbuilder
```
#Debian Sid
$sudo pbuilder build --basetgz /var/cache/pbuilder/base-sid-amd64.tgz \
      --distribution sid foobar*.dsc

#Debian Stable
$sudo pbuilder build --basetgz /var/cache/pbuilder/base-stable-i386.tgz \
      --distribution stable foobar*.dsc

#Ubuntu Raring
$sudo pbuilder build --basetgz /var/cache/pbuilder/base-raring-amd64.tgz \
      --distribution raring foobar*.dsc
```

Nas primeiros vezes que você usa o pbuilder é comum assinar com gpg (um
tipo de programa de criptografia) os arquivos gerados manualmente como o
**debsign**.

```
$debsign -kfoo@bar.io /var/cache/pbuilder/result/foobar*.dsc
$debsign -kfoo@bar.io /var/cache/pbuilder/result/foobar*.changes
```

Ou usar um **pdebuild** para gerar o pacote e assinar os arquivos
**.dsc** e **.changes** automagicamente. =)

```
# Sid
$sudo pdebuild --auto-debsign --debsign-k XXXXXXXX --  \
      --basetgz /var/cache/pbuilder/base-sid-amd64.tgz --distribution sid \
      foobar*.dsc

# Stable i386
$sudo pdebuild --auto-debsign --debsign-k XXXXXXXX --  \
      --basetgz /var/cache/pbuilder/base-stable-i386.tgz \
      --distribution stable --architecture i386 foobar*.dsc

# Ubuntu Raring
$sudo pdebuild --auto-debsign --debsign-k XXXXXXXX --  \
      --basetgz /var/cache/pbuilder/base-raring-amd64.tgz \
      --distribution raring  --mirror http://ftp.ubuntu.com/ubuntu \
      foobar*.dsc
```

Atualizando ambientes chroot
----------------------------

Se precisar atualizar esses ambientes criados, pode fazê-los como os
exemplos abaixo.

```
# Debian Sid
$pbuilder update --basetgz /var/cache/pbuilder/base-sid-amd64.tgz \
      --distribution sid

# Debian Stable i386
$pbuilder update --basetgz /var/cache/pbuilder/base-stable-i386.tgz \
      --distribution stable --architecture i386

# Ubuntu Raring
$pbuilder update --basetgz /var/cache/pbuilder/base-raring-amd64.tgz \
      --distribution raring
```

Os arquivos e o pacotes depois de gerados pelo pdebuild ou pbuilder
estarão em ”*/var/cache/pbuilder/result/*”. Mas você pode mudar isso
facilmente usando a opção *–buildresult*, olhe o manual do pbuilder.

Conclusão
---------

O pbuilder e pdebuild são excelentes ferramentas que podem ser
utilizadas de muitas formas diferentes, principalmente para automação de
testes. Se quiser saber mais, leia manuais dos dois (*\$man pbuilder*,
*man pdebuild*) ou se quiser automatizar pode ler as wiki do
[Debian](https://wiki.debian.org/PbuilderTricks) e
[Ubuntu](https://wiki.ubuntu.com/PbuilderHowto) (recomendadíssmo).
