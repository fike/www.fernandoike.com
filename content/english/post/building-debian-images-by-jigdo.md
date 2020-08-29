+++
title = "Building Debian images by jigdo"
date = "2015-08-19"
draft = false
categories = ["SL", "english", "debian"]
tags = ["english", "debian", "jigdo", "images", "english", "SL"]
+++
A friend asked me how to got a [Debian][debian] Old Image, she wanted to download Debian [Squeeze][squeeze] DVD image. Unfortunately, it's impossible to download by Debian-CD mirror because Squeeze isn't more maintainer. So, it's possible to get a Image by Debian-CD primary server but it's locate in Sweden. Nothing problem, right? Well, She lives in Brazil and the download time is a little bit more than 8 hours.

A good tool to "download" a Debian image is the [Jigdo][jigdo]. It's a program to synchronize repositories and generate Images. It get packages and build a image locally in your computer.

I made a simple test, I used jigdo to "download" the first Squeeze DVD by brazilian repository (Unicamp) and compare with a download image by PR (Primary Server). The difference was huge, PS download took a long time to finish (8 hours) and Unicamp mirror finished in 100 minutes.

Well, let's go to practice.

### Install jigdo
```
#aptitude install jigdo
```

### Downloading and building image

The jigdo file (.jigdo) is simple list with all packages and hash of a instalation image. You need it to start the downloads. In this case, I used jigdo file to build first Squeeze DVD.

```
$jigdo-lite http://cdimage.debian.org/cdimage/archive/6.0.10/amd64/jigdo-dvd/debian-6.0.10-amd64-DVD-1.jigdo
```

Before to begin download, jidgo need some arguments. Fill arguments of your preference but remember that the argument more important is the mirror. If you have doubt what's mirror is more fast, you can use [netselect-apt][1] to discovery. For my test, I'm used Unicamp mirror ([http://debian.las.ic.unicamp.br/debian][unicampmirror]).

#### My jigdo-lite conf file.

```

$cat ~/.jigdo-lite
-------
jigdo=''
debianMirror='http://debian.las.ic.unicamp.br/debian/'
nonusMirror=''
tmpDir='.'
jigdoOpts='--cache jigdo-file-cache.db'
wgetOpts='--passive-ftp --dot-style=mega --continue --timeout=30'
scanMenu='
```


Nice, huh?

Take a coffee and forget to download Debian images using others programs (**curl**, **wget**, etc.). :)

[squeeze]: https://www.debian.org/releases/squeeze/
[debian]: http://www.debian.org/
[jigdo]: https://www.debian.org/CD/jigdo-cd/
[unicampmirror]: http://debian.las.ic.unicamp.br/debian
[1]: https://packages.debian.org/search?keywords=netselect-apt
