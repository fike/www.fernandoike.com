+++
title = "Pbuilder and pdebuild to sign deb package automagically"
date = "2013-09-20"
draft = false
Categories = ["portugues", "SL", "debian"]
Tags = ["portugues", "debian", "Pbuilder", "packaging"]
+++
To create a deb package (debian way) it is hard work. After spending
some time working on that, you will feel more comfortable but the
package building still is a little bit complex. Mainly if you add tests.

A good tool to create a deb package automatically is
[pbuilder](http://www.netfort.gr.jp/~dancer/software/pbuilder-doc/pbuilder-doc.html).
It creates a chroot jail and it allows to build deb packages for
[Debian](http://www.debian.org) and [Ubuntu](http://www.ubuntu.com).

Create chroot jails environment
-------------------------------

Debian Sid/Unstable em AMD64
```
$sudo pbuilder create --basetgz /var/cache/pbuilder/base-sid-amd64.tgz \
    --distribution sid
```

Debian Wheezy (Stable) I386 (ia32)
```
$sudo pbuilder create --basetgz /var/cache/pbuilder/base-stable-i386.tgz \
    --distribution stable --architecture i386
```

If you are using Debian and you want to build a deb package to Ubuntu.
It can be done adding the Ubuntu repository public key in apt keyring
before pbuilder use. Bellow is an example with Ubuntu Raring Ringtail
(13.04).

```
$sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 3B4FE6ACC0B21F32

$sudo pbuilder create --basetgz /var/cache/pbuilder/base-raring-amd64.tgz \
    --distribution raring --mirror http://ftp.ubuntu.com/ubuntu \
    --debootstrapopts --keyring=/etc/apt/trusted.gpg
```

Building packages
-----------------

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

The files and deb packages built are at ”*/var/cache/pbuilder/result/*”.
But it can easly be changed using *–buildresult* option, take a look at
pbuilder manual for more details.

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

Updating chroot environment
---------------------------

If one needs to update these created chroots, it can be done as the
examples bellow.

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
The files and deb packages built are at ”*/var/cache/pbuilder/result/*”.
But it can easly be changed using *–buildresult* option, take a look at
pbuilder manual for more details.

Conclusion
----------

Pbuilder and pdebuild are good tools that can be used in many ways,
mainly to build tests automation. If you want to know more, take a look
at manuals (*\$man pbuilder*, *man pdebuild*) and you can find good tips
about automation building in
[Debian](https://wiki.debian.org/PbuilderTricks) and
[Ubuntu](https://wiki.ubuntu.com/PbuilderHowto) wiki.
