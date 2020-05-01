+++
title = "Debian adicionando novas fontes manualmente"
date = "2013-03-21"
draft = false
categories = ["debian", "portugues", "SL"]
tags = ["debian", "fontes", "portugues"]
+++
Esses dias precisei algumas fontes que não estão empacotadas para o
Debian e entre as várias maneiras de instalar, a que maneira mais
simples (para mim) foi usar o fc-cache para instalar.

```
$mkdir ~/.fonts
$cp \*.ttf ~/.fonts
$cd ~/.fonts
$fc-cache
```

Ah… Claro, o fc-cache está no pacote fontconfig, então você precisa
desse pacote para usá-lo. ;)
