+++
title = "Docker 1 dot 3"
date = "2014-10-23"
draft = false
Categories = ["docker ", "SL", "portugues"]
Tags = ["portugues", "docker", "SL", "programming", "foss", "C", "ruby", "go", "go lang", "java", "php", "docker hub"]
+++
![]( /images/solomon-keynote-penguin-authentication-300x235.png)

A [versão 1.3][docker13] do [Docker][docker] foi lançada recentemente. Eu
gostei dela por duas razões.

## Verificação da assinatura digital

O pessoal da DotCloud já tinha [anunciado][danuncio] alguns repositórios
oficiais de alguma ferramentas e linguagens de programação (**C(++)/GCC**,
**PHP**, **Go**, **Java**, **Nodejs**, **Python**, **Perl**, **Ruby**,
etc.). O Docker verifica se os repositórios oficiais estão íntegros, eles
(os repositórios) são assinados com chave criptográficas. (Obs. procurando
que tipos de chaves são e como são assinados)

Antes disso eu tinha um pouco de restrição com os repositórios de terceiros.
Até então, preferia criar meus templates de containers.

## Entrar num container em execução

Nas versões anteriores era um pouco trabalhoso para você entrar num container
e analisar um problema que estivesse ocorrendo, exemplo: identificar um
problema de permissão num diretório.

Na versões anteriores teria que ser feito assim:

Na criação do container deveria compartilhar os diretórios de log e da
aplicação. Supondo que seja um servidor web simples, o  dockerfile seria
como o abaixo:

```

FROM debian:wheezy

MAINTAINER fike at midstorm.org

RUN apt-get udpate && apt-get install apache2

ADD mysite /var/www/

RUN apt-get autoremove -y && rm -rf /tmp/* /var/tmp/

ENV APACHE_RUN_USER www-data

ENV APACHE_RUN_GROUP www-data

ENV APACHE_LOG_DIR

VOLUMES ["/var/log/apache2", "/var/www"]

CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]

```

### Criando o container

```

fike@kamino:~$ docker build -t="mysimplesite"  .

```

### Executando

```

fike@kamino:~$ sudo docker run -d -p  80:80 mysimplesite

```

### Putz! Os internautas não estão conseguindo acessar meu site, ele está retornando 403.

Se não tiver uma versão mais recente do util-linux (> 2.27)
[não poderá usar][nsenter] o nsenter. Outra forma seria executar um segundo
container e acessar os diretórios compartilhados do primeiro.

```
fike@kamino:~$ CONTAINERID=$(docker ps |grep mysimplesite|awk '{ print $1}'

fike@kamino:~$ docker run -it --volumes-from=$CONTAINERID /bin/bash

```

Se estiver usando um [Fluent][fluent] ou outro agregador de logs não
precisaria disso, certo? Nesse caso, sim. Entretanto pode ocorrer de precisar
inspecionar um container para verificar um vazamento de memória ou algo
que necessite analisar a aplicação em produção.

Se o problema estiver relacionado a rede, a abordagem era parecida. Um bom
exemplo, alterar uma zona DNS no Bind9 usando o **rndc**.

```
fike@kamino:~$ CONTAINERID=$(docker ps |grep mysimplesite|awk '{ print $1}'

fike@kamino:~$ docker run -it --volumes--from=$CONTAINERID --net='container:$CONTAINERID' mysimplesite /bin/bash

```

No 1.3 é bem mais simples.

```
fike@kamino:~$ CONTAINERID=$(docker ps |grep mysimplesite|awk '{ print $1}'

fike@kamino:~$ docker exec -it $CONTAINERID /bin/bash
```

[docker13]: https://blog.docker.com/2014/10/docker-1-3-signed-images-process-injection-security-options-mac-shared-directories/
[danuncio]: https://blog.docker.com/2014/09/docker-hub-official-repos-announcing-language-stacks/
[docker]: http://www.docker.com
[nsenter]: http://jpetazzo.github.io/2014/03/23/lxc-attach-nsinit-nsenter-docker-0-9/
[fluent]: http://www.fluentd.org/
