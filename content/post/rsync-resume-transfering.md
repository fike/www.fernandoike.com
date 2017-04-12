+++
title = "Rsync resume transfering"
date = "2012-10-25"
draft = false
Categories = ["debian", "linux", "SL", "english"]
Tags = ["english", "debian", "rsync", "SL", ]
+++
![](/images/i-robot-300x165.jpg)

My memory has some bugs and  I often forget command syntax and other
things. ;)

Frequently, I have synchronized VMs images in some datacenters. The
internet in Brazil is “lazy” when compared to some other countries,
mainly to upload traffic. The max upload transfer in my house  is
120kbits and VM image is more or less 4Gb, then you imagine how long it
is necessary to complete an upload!

I would bet it takes a little more than 11 hours to complete. This when
some interruption internet connection. =/

Well, let’s go:

```
$rsync -CravzpP --progress  ozzy_sane.img user@domain.dom:~
```

The magic option is ”**P**”. It is an abbreviation[](http://www.fernandoike.com/wp-content/uploads/2012/10/i-robot.jpg) to**Preserve**.  If there are still some remaining doubts, *read the manual*. ;)
