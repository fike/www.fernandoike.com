+++
title = "Adicionando legenda ao video por linha de comando"
date = "2013-09-13"
draft = false
Categories = ["portugues", "debian", "SL"]
Tags = ["portugues", "debian", "SL", "ffmpeg", "avconv"]
+++
O libav é um fork do ffmpeg e tem a maioria das funcionalidades do
ffmpeg. Como libav é um pacote oficial do Debian, ele será usado como a
ferramenta para adicionar as legendas mas a sintaxe funciona com o
ffmpeg.

Para adicionar uma legenda é necessário usar o avconv que está includo
no pacote libav-tools.

```
$sudo aptitude install libav-too
```

Para adicionar, basta executar o avconv com a opção *-vf subtitles*.

```
$avconv -i foobar.ogv -vf subtitles=foobar.srt foobar-subtitle.ogv
```
