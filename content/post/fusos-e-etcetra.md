+++
title = "Fusos e etcetra"
date = "2014-05-20"
draft = false
Categories = ["SL", "debian", "portugues"]
Tags = ["portugues", "SL", "timezone", "debian"]
+++
![]( /images/Tz_world_2013i_efele.png)

Algum tempo atrás usava um relatório de um serviço em que o se você
mudasse fuso horário (timezone) do relatório de GMT (0) para o horário
brasileiro. Ao invés de trocar de GMT para GMT *-3* e diminuir três
horas, na verdade mudava para *+3*.

Exemplo: Se no Brasil (sem horário de verão e horário de Brasília) fosse
*16 horas*, GMT seria *19*. Mas no relatório apresentava *22 horas*.

O detalhe é que na opção para mudar só tinha opção Etc/GMT *-3*.

Em sistemas Unix/Linux, **Etc** é um subdiretório
(*/usr/share/zoneinfo/Etc*). Ele serve de referências de fuso horário
para [regiões não habitadas](ftp://ftp.iana.org/tz/data/etcetera).

Então, porque usar *+3* ao invés de *-3*?

Aprendi nas aulas de geografia que o estado de São Paulo está no
*UTC-03:00*. Estamos acostumados usar como referência o sinal de menos,
exemplo: “Rio de Janeiro está 3 horas atrás (-3) de Londres. Se Londres
for 5 horas, o horário no Rio de Janeiro será 2 horas.”. Entretanto isso
é um pouco diferente em sistemas operacionais baseados na
[POSIX](https://en.wikipedia.org/wiki/POSIX).

Na POSIX, os fusos horários que estão do lado Oeste ao GMT tem o sinal
positivo (+) e os que estão à Leste tem o sinal negativo (-).

Com o date e a variável de ambiente **TZ** pode-se brincar um pouco:

```

#GMT
fike@klatoon:~$ TZ='GMT' date
Sex Mai 16 20:35:03 GMT 2014

#UTC -3
fike@klatoon:~$ TZ='GMT+3' date -R
Fri, 16 May 2014 17:35:03 -0300

#UTC +3
fike@klatoon:~$ TZ='GMT-3' date -R
Fri, 16 May 2014 23:35:03 +0300

#Brasil Leste
fike@klatoon:~$ TZ='Brazil/East' date
Sex Mai 16 17:35:03 BRT 2014

#Brasil Oeste
fike@klatoon:~$ TZ='Brazil/West' date
Sex Mai 16 16:35:03 AMT 2014

#São Paulo
fike@klatoon:~$ TZ='America/Sao_Paulo' date
Sex Mai 16 17:35:03 BRT 2014

#Rio Branco - Acre
fike@klatoon:~$ TZ='America/Rio_Branco' date
Sex Mai 16 15:35:03 ACT 2014

#Brasil
fike@klatoon:~$ TZ='Brazil/East+3' date
Sex Mai 16 20:35:03 Brazil 2014

#São Paulo
fike@klatoon:~$ TZ='America/Sao_Paulo+3' date
Sex Mai 16 20:35:03 America 2014

#Cuiaba
fike@klatoon:~$ TZ='America/Cuiaba' date
Sex Mai 16 16:35:03 AMT 2014

#Cuiaba
fike@klatoon:~$ TZ='America/Cuiaba+4' date
Sex Mai 16 20:35:03 America 2014

#Araguaina
fike@klatoon:~$ TZ='America/Araguaina' date
Sex Mai 16 17:35:03 BRT 2014

#Fernando de Noronha
fike@klatoon:~$ TZ='America/Noronha' date
Sex Mai 16 18:35:16 FNT 2014
```

Para saber quais são as cidades ou regiões que pode usar no **TZ**, olhe
no ”**/usr/share/zoneinfo**” que tem outros. Para saber todas as cidades
brasileiras que são possíveis de usar no TZ, procure no arquivo
[zone.tab](http://en.wikipedia.org/wiki/Zone.tab) no
[tzdata](http://www.iana.org/time-zones) que é disponibilizado na
[IANA](http://www.iana.org/). [Uma versão
dele](http://en.wikipedia.org/wiki/Zone.tab) pode ver na Wikipedia.

Portanto, fusos horários no horário padrão ([standard
time](http://en.wikipedia.org/wiki/Time_standard)) que estão à Oeste de
[UTC](http://pt.wikipedia.org/wiki/Tempo_Universal_Coordenado) ou
[GMT](http://pt.wikipedia.org/wiki/Greenwich_Mean_Time) tem o sinal
negativo (-) e os fusos à Leste que estão à Leste tem o sinal positivo.
Mas quando você tem que ajustar o fuso horário num sistema Unix/Linux,
lembre-se que o sinal é ao contrário; Oeste é positivo (+) e Leste é
negativo (-).

Na lista
[debian-user](https://lists.debian.org/debian-user/2013/01/msg01133.html)
tem uma thread com uma boa explicação sobre o tema também recomendável
ler o artigo na Wikipedia sobre os [fusos horários no
Brasil](http://en.wikipedia.org/wiki/Time_in_Brazil) (em inglês que é
mais datalhado).

Obs. Imagem da Wikipedia, a original pode ser acessada
[aqui](http://commons.wikimedia.org/wiki/File:Tz_world_2013i_efele.png).
