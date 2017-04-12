+++
title = "Purge Debian packages marked with rc status"
date = "2014-09-12"
draft = false
Categories = ["debian", "english", "SL"]
Tags = ["english", "debian", "dpkg", "SL"]
+++
Sometimes when I find a package that is installed on my computer ([Debian][debian]), I
found status **rc** but I never found a explanation in official documentation.

For now, my OS has the following packages marked **rc** status:
```
fike@klatoon:~$ dpkg -l | grep ^[rc]

rc  libaacplus2:i386                      2.0.2-dmo1                            i386         AAC+ encoding library - runtime files
rc  libavcodec55:i386                     10:2.3.3-dmo3                         i386         Library to encode decode multimedia streams - runtime files
rc  libavresample1:i386                   10:2.3.3-dmo3                         i386         FFmpeg audio conversion library
rc  libavutil52:i386                      10:2.3.3-dmo3                         i386         FFmpeg avutil library - runtime files
rc  libavutil53:i386                      6:10.4-1                              i386         Libav utility library
rc  libcrystalhd3:i386                    1:0.0~git20110715.fdd2f19-11          i386         Crystal HD Video Decoder (shared library)
rc  libfaac0:i386                         1:1.28-dmo3                           i386         AAC audio encoder - library files.
rc  libfdk-aac0:i386                      1:0.1.3-dmo1                          i386         Fraunhofer FDK AAC codec library.
rc  libfftw3-long3:amd64                  3.3.4-1                               amd64        Library for computing Fast Fourier Transforms - Long precision
rc  libgssglue1:amd64                     0.4-2                                 amd64        mechanism-switch gssapi library
rc  libjim0.74:amd64                      0.74-3                                amd64        small-footprint implementation of Tcl - shared library
rc  liblcms1:i386                         1.19.dfsg2-1.5                        i386         Little CMS color management library
rc  libmkv0:amd64                         0.6.5.1-dmo3                          amd64        Alternitave to the official libmatroska/libebml libraries.
rc  libmp4v2-2:amd64                      2:2.0.0-dmo2                          amd64        MP4 container library - runtime files
rc  libswresample0:i386                   10:2.3.3-dmo3                         i386         FFmpeg audio rescaling library
rc  libupower-glib2:amd64                 0.99.0-3                              amd64        abstraction for power management - shared library
rc  libx265-25:amd64                      1.2-dmo1                              amd64        x264 video coding library.
rc  libx265-25:i386                       1.2-dmo1                              i386         x264 video coding library.
rc  libx265-31:i386                       1.3-dmo1                              i386         x264 video coding library
rc  libzvbi0:i386                         0.2.35-2                              i386         Vertical Blanking Interval decoder (VBI) - runtime files
rc  pcmciautils                           018-8                                 amd64        PCMCIA utilities for Linux 2.6

fike@klatoon:~$

```

Let us pick pcmciautils package as example. Checking if it doesn't be installed on my OS.

```

fike@klatoon:~$ dpkg -L pcmciautils
Package `pcmciautils' does not contain any files (!)

fike@klatoon:~$
```

Now, opening "/var/lib/dpkg/status" file, here has the status all packages existents and search pcmciautils package status.

```
...
Package: pcmciautils
Status: deinstall ok config-files
Priority: extra
Section: admin
...
```

A little strange "deinstall ok config-files" as status, right? Well, it's more easy to understand. Checking again dpkg manual...



```
fike@klatoon:~$man dpkg
...
   Package selection states
       install
              The package is selected for installation.

       hold   A package marked to be on hold is not handled by dpkg, unless forced to do that with option --force-hold.

       deinstall
              The package is selected for deinstallation (i.e. we want to remove all files, except configuration files).
...
```

Gotcha! Its more easy to understand. To pcmciautils packages, the **rc** status is because its removed and still has the configuration file.

```
fike@klatoon:~$ find /etc/ /var/ -name "*pcmcia*" -print 2> /dev/null
/etc/pcmcia
/var/lib/dpkg/info/pcmciautils.list
/var/lib/dpkg/info/pcmciautils.postrm
fike@klatoon:~$

```

The finally, removing all packages with **rc** status.

```
root@klatoon:~# aptitude purge $(dpkg -l|grep ^[rc] | awk '{ print $2}')
The following packages will be REMOVED:  
  libaacplus2:i386{p} libavcodec55:i386{p} libavresample1:i386{p} libavutil52:i386{p} libavutil53:i386{p} libcrystalhd3:i386{p} libfaac0:i386{p}
  libfdk-aac0:i386{p} libfftw3-long3{p} libgssglue1{p} libjim0.74{p} liblcms1:i386{p} libmkv0{p} libmp4v2-2{p} libswresample0:i386{p} libupower-glib2{p}
  libx265-25{p} libx265-25:i386{p} libx265-31:i386{p} libzvbi0:i386{p} pcmciautils{p}
0 packages upgraded, 0 newly installed, 21 to remove and 4 not upgraded.
Need to get 0 B of archives. After unpacking 0 B will be used.
Do you want to continue? [Y/n/?]
(Reading database ... 214094 files and directories currently installed.)
Removing libaacplus2:i386 (2.0.2-dmo1) ...
Purging configuration files for libaacplus2:i386 (2.0.2-dmo1) ...
Removing libavcodec55:i386 (10:2.3.3-dmo3) ...
Purging configuration files for libavcodec55:i386 (10:2.3.3-dmo3) ...
Removing libavresample1:i386 (10:2.3.3-dmo3) ...
Purging configuration files for libavresample1:i386 (10:2.3.3-dmo3) ...
Removing libavutil52:i386 (10:2.3.3-dmo3) ...
Purging configuration files for libavutil52:i386 (10:2.3.3-dmo3) ...
Removing libavutil53:i386 (6:10.4-1) ...
Purging configuration files for libavutil53:i386 (6:10.4-1) ...
Removing libcrystalhd3:i386 (1:0.0~git20110715.fdd2f19-11) ...
Purging configuration files for libcrystalhd3:i386 (1:0.0~git20110715.fdd2f19-11) ...
Removing libfaac0:i386 (1:1.28-dmo3) ...
Purging configuration files for libfaac0:i386 (1:1.28-dmo3) ...
Removing libfdk-aac0:i386 (1:0.1.3-dmo1) ...
Purging configuration files for libfdk-aac0:i386 (1:0.1.3-dmo1) ...
Removing libfftw3-long3:amd64 (3.3.4-1) ...
Purging configuration files for libfftw3-long3:amd64 (3.3.4-1) ...
Removing libgssglue1:amd64 (0.4-2) ...
Purging configuration files for libgssglue1:amd64 (0.4-2) ...
Removing libjim0.74:amd64 (0.74-3) ...
Purging configuration files for libjim0.74:amd64 (0.74-3) ...
Removing liblcms1:i386 (1.19.dfsg2-1.5) ...
Purging configuration files for liblcms1:i386 (1.19.dfsg2-1.5) ...
Removing libmkv0:amd64 (0.6.5.1-dmo3) ...
Purging configuration files for libmkv0:amd64 (0.6.5.1-dmo3) ...
Removing libmp4v2-2:amd64 (2:2.0.0-dmo2) ...
Purging configuration files for libmp4v2-2:amd64 (2:2.0.0-dmo2) ...
Removing libswresample0:i386 (10:2.3.3-dmo3) ...
Purging configuration files for libswresample0:i386 (10:2.3.3-dmo3) ...
Removing libupower-glib2:amd64 (0.99.0-3) ...
Purging configuration files for libupower-glib2:amd64 (0.99.0-3) ...
Removing libx265-25:i386 (1.2-dmo1) ...
Purging configuration files for libx265-25:i386 (1.2-dmo1) ...
Removing libx265-25:amd64 (1.2-dmo1) ...
Purging configuration files for libx265-25:amd64 (1.2-dmo1) ...
Removing libx265-31:i386 (1.3-dmo1) ...
Purging configuration files for libx265-31:i386 (1.3-dmo1) ...
Removing libzvbi0:i386 (0.2.35-2) ...
Purging configuration files for libzvbi0:i386 (0.2.35-2) ...
Removing pcmciautils (018-8) ...
Purging configuration files for pcmciautils (018-8) ...

root@klatoon:~#

```

### Updating

@kretcheu saw by twitter another and best command to remove these packags.

```
#aptitude ~c
```

P.S. I know, I could went directly the final but it's cool understand why of the things. :)

[debian]: http://www.debian.org
