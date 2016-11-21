+++
title = "Cedilha com teclado americano"
date = "2013-04-09"
draft = false
Categories = ["debian", "portugues", "SL"]
Tags = ["teclado", "debian", "portugues", "gnome"]
+++
Troquei a localização do idioma do meu [Gnome](http://www.gnome.org)
para inglês e ao reiniciar a sessão o **ç** não funcionou mais.
Aparentemente isso acontece porque o mapa americano (EUA) do teclado
**us\_intl** está com **ć** ao invés de **ç**.

Se usar Gnome ([GTK](http://www.gtk.org)) ou [KDE](http://www.kde.org)
([QT](http://qt-project.org)) é relativamente fácil resolver. Se tiver
problema com outras bibliotecas gráficas terá que mudar o mapa do
teclado no [XOrg](http://x.org).

Pode simplesmente acrescentar as linhas abaixo em /etc/environment.

```
GTK_IM_MODULE=cedilla
QT_IM_MODULE=cedilla
```
