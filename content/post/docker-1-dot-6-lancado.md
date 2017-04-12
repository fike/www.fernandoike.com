+++
title = "Docker 1 dot 6 lancado"
date = "2015-04-27"
draft = false
Categories = ["debian", "docker", "SL", "portugues", "devops"]
Tags = ["docker", "container", "SL", "portugues", "debian", "jessie", "backports"]
+++
![]( /images/docker-1.6.png)

O lançamento da versão 1.6 veio com boas novidades, algumas delas são do
ecossistema mas cabe destacar: [Docker Compose][compose], [Docker Machine][machine]
e o [Registry][registry]. O Compose é o antigo [Fig][fig], ele facilita bastante
se você trabalho com sistemas em múltiplos containers. O Machine permite
criar uma infraestrutura Docker rapidamente, seja numa máquina virtual
(exemplo: Virtualbox) ou mesmo numa IaaS (AWS, Digital Ocean, etc.).

As funcionalidades da versão 1.6 que gostei foram:

## Suporte a Image Labels
No Dockerfile pode adicionar um campo extra para usar como identificação sua.
Isso permite pesquisar informações de containers e imagens usando esse campo.

## Logging Drivers
Ficou bem mais fácil enviar os logs para um Syslog ou similares. Muita gente
tem dificuldade de lidar com os logs do container até essa versão.

- Alterar as imagens de containers sem recriá-las
A partir desta versão é possível alterar algumas coisas numa imagem de
container sem a necessidade de gerar novamente.

## Ulimit
A minha favorita, agora é possível alterar alguns parâmetros do ulimit,
bom para serviços que usam muito processos como banco de dados.

Para saber mais, acesse [o blog][blogdocker] do Docker que tem mais informações.

Obs.: Ah, a versão 1.6 está na *Experimental* no Debian e infezlimente não
[entrou][bugdebian] na Jessie, mas logo estará disponível no [Backports][backports].

Obs.2: O original dessa [imagem][imagem] é do blog do Docker.

[compose]: https://docs.docker.com/compose/
[machine]: https://docs.docker.com/compose/
[registry]: https://docs.docker.com/registry/
[fig]: http://www.fig.sh/
[bugdebian]: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=781554
[blogdocker]: https://blog.docker.com/2015/04/docker-release-1-6/
[backports]: http://backports.debian.org/
[imagem]: http://blog.docker.com/media/2015/04/docker-1.6.png
