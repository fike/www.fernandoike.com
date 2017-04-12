+++
title = "Adding subtitles to video using shell"
date = "2013-09-13"
draft = false
Categories = ["SL", "debian", "english"]
Tags = ["english", "SL", "debian", "avconv", "ffmpeg"]
+++
The libav is a ffmpeg fork and it has the most ffmpeg features. As libav
is an official Debian package, it will be used like a tool to add
subtitles but it works like a ffmpeg.

To add a subtitle to video, it’s needed to use avconv that is included
in libav-tools package. So, let’s install it.

```
$sudo aptitude install libav-tools
```

So, it’s simple to add subtitles to a video.

```
avconv -i foobar.ogv -vf subtitles=foobar.srt foobar-subtitle.ogv
```
