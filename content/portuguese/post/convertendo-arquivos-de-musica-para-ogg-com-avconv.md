+++
title = "Convertendo arquivos de musica para ogg com avconv"
date = "2013-11-23"
draft = false
categories = ["SL", "debian", "portugues"]
tags = ["portugues", "avconv", "debian", "ffmpeg"]
+++
Eu estava recuperando os arquivos do **Navaranda Podcast** para deixar
disponível na internet. A versão original estava no formato
[WAV](https://pt.wikipedia.org/wiki/WAV) e minha intenção era converter
todos para o formato [OGG](https://www.vorbis.com/). Para fazer isso,
usei o [avconv](https://libav.org/avconv.html) (um fork do
[ffmpeg](https://www.ffmpeg.org/)) e diminiu o bitrate para **6kbits/s**.

Primeiramente instalando o *avconv*.

```
#aptitude install avconv
```

```
$for i in $(echo *.wav)
  do avconv -i $i -acodec libvorbis -b:a 64k ${i%%.wav}.ogg
done
```

Ah, já ia esquecendo! Isso foi feito no Debian. ;)
