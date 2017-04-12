+++
title = "Timeout para instalar pacotes no Debian velho"
date = "2012-12-28"
draft = false
Categories = ["SL", "debian", "portugues"]
Tags = ["portugues", "SL", "debian", "lenny"]
+++
![](/images/debian-lenny.jpg)

Lembra de um outro
[post](http://www.fernandoike.com/2012/12/27/instalando-um-debian-velho-lenny/)
sobre a instalação do [Debian](http://www.debian.org) de um versão
antiga?

Então, continuando a saga…

Um dos repositórios que estou usando não tem uma taxa de transferência
muito alta. então alguns pacotes tem apresentado o erro abaixo:

    ...Operation timed out after 120000 milliseconds with 26312704 out of 62820482 bytes received...

Isso é fácil de resolver, basta acrescentar um parâmetro na configuração
do apt.conf para forçar o tempo de expiração de baixar arquivos para
maior que o padrão (120 segundos).

    #echo "Acquire::http::Timeout "600";" >> etc/apt/apt.conf.d/02timeout
