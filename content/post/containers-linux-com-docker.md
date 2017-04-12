+++
title = "Containers linux com docker"
date = "2014-06-30"
draft = false
Categories = ["debian", "timbira", "SL", "portugues"]
Tags = ["portugues", "debian", "docker", "SL", "containers"]
+++
![docker_logo.png](/images/docker_logo.png)

[Docker][1] é provavelmente o novo buzzword depois do [OpenStack][2] (se você
lembrar de outro, comenta aí.). O Docker é desenvolvido em [Go][3] e
usa a Apache License, ele algumas funcionalidades interessantes ao
[LXC][4] como um repositório público de containers,
DSL(Domain-Specific Language) bem simplicado para criar containers e
fazer commit (como svn commit ou git commit) das alterações dos containers.

A página de manual do Docker tem uma explicação melhor que a minha.

*Docker complementa o LXC, atuando como uma API de alto nível no nível de processo.
Ele executa processos unix com forte garantia de isolamento e repetibilidade
nos servidores.

O conceito de container é antigo no universo Unix/Linux e várias
"implementações", antes de virtualização ser amplamente usado era muito comum
usar chroot para prover isolamento de serviços (BIND, Postfix, etc.).
Outros tipos de containers muito usados no Linux são OpenVZ e Vserver mas
nenhum deles teve uma adoção em massa tão grande como o Docker. Isso porque
ele facilitou muito o trabalho para criar e manter os containers. Essas
são alguns razões porque ele tem sido adotado por muitas empresas como:
Googe, Red Hat, Baidu, Ebay, Yandex, Spotify, Canonical, etc.

A instalação, atualmente, é bem relativamente simples. A maioria das
distribuições Linux suporta de alguma forma. No [Debian][5] está disponível
nos repositórios oficiais para [Sid][6] e [Jessie][7] (a próxima versão
estável).

Se quiser instalar o Docker no [Wheezy][8] (atual versão estável)
terá que usar os pacotes mantido pela equipe do Docker e usar o kernel
linux acima da versão 3.8. Provavelmente terá que usar o repositório
Backports para isso, então terá que acrescentar no arquivo sources.list.

```
root@kamino:~ echo "http://http.debian.net/debian/ wheezy-backports main non-free contrib" >> /etc/apt/sources.list.d/backports.list

root@kamino:~ aptitude update

root@kamino:~ aptitude -t wheezy-backports install linux-image-amd64 linux-headers-amd64
```

Os textos na internet mostram duas formas de instalar no Wheezy, uma usando
o Docker empacotado para o Ubuntu e a outra baixando o binário diretamente
do site do Docker.

```
#wget https://get.docker.io/builds/Linux/x86_64/docker-latest -O /usr/local/bin/docker
```

Mais detalhes de como instalar no Wheezy, recomendo ler os textos no [Debian
Administration][9].

No Jessie e no Sid, basta instalar via aptitude.

```
#aptitude install docker.io
```

O restante do texto e outros poderão ser escritos num futuro próximo, será
usado como referência o Docker do repositório oficial do Debian.

O Docker tem um repositório público onde qualquer pode disponibilizar
container para qualquer um usar. Algumas empresas estão suportando
oficialmente seus produtos no Docker (Ubuntu e CentOS). Além dos
repositórios oficiais tem uma grande variedade de container disponíveis,
pode usá-las para testar softwares ou se confiar no autor do container
usá-las para disponibilizar rapidamente um servidor JBoss, MongoDB,
PostgreSQL, etc.

Para pesquisar os containers disponíveis é usando o **search**.

```
$docker.io search postgresql | head -n10

NAME                     DESCRIPTION                                     STARS  OFFICIAL  AUTOMATED
postgres                 PostgreSQL is a powerful, open source obje...   65                   
paintedfox/postgresql    A docker image for running Postgresql.          30                 [OK]
atlassian/jira           Atlassian Jira image with Postgresql.           11                 [OK]
helmi03/docker-postgis   PostGIS 2.1 in PostgreSQL 9.3                   9                  [OK]
zaiste/postgresql        PostgreSQL 9.2 - https://gist.github.com/z...   8                    
zumbrunnen/postgresql    PostgreSQL from apt.postgresql.org              6                  [OK]
orchardup/postgresql     https://github.com/orchardup/docker-postgr...   6                  [OK]
kamui/postgresql         PostgreSQL 9.3 with configurable login/dat...   5                  [OK]
tutum/postgresql         PostgreSQL Docker Image – listens on po...      4                  [OK]
[...]
```

No retorno do comando, alguns campos relevantes são *NAME*, *STAR* e
*AUTOMATED*. NAME com "/" é dono do repositório e o nome do repositório,
o STAR é o números de pessoas que marcaram como destaque o repositório
e AUTOMATED é se o container foi criado automaticamente ou não. Talvez este
seja o mais interessante ou "auditável" porque ele é gerado por um arquivo
com os passos para criar o container que foi publicado no Github ou Bitbucket.

Se quiser um container usando o Debian como base, tem duas formas. Uma usando
o repositório "semi-oficial" e a outra é você usando o [debootstrap][11]. Alguns
desenvolvedores do Debian não recomendam usar o repositório semi-oficial
porque ele está ligeiramente diferente da versão via debootstrap.
Recomendo leitura do [texto][10] do Joey Hess que tem um ponto de vista interessante.

Pela simplicidade de usar containers com o Docker, pode-se esquecer alguns aspectos de
segurança, então é recomendado fortemente ler o texto ["CONTAINERS & DOCKER: HOW
SECURE ARE THEY?"][12] no blog do Docker e também a [página de segurança][13] na
documentação oficial

Docker é uma das coisas mais legais que pude me envolver um pouco mais nos
últimos tempos mas é importante lembrar que ele não é (e nem pode ser
considerado) a nova bala de prata.

[1]: http://www.docker.com
[2]: https://www.openstack.org
[3]: http://golang.org/
[4]: https://linuxcontainers.org/
[5]: http://www.debian.org
[6]: http://www.debian.org/releases/sid/
[7]: http://www.debian.org/releases/jessie/
[8]: http://www.debian.org/releases/wheezy/
[9]: http://debian-administration.org/article/696/A_brief_introduction_to_using_docker
[10]: http://joeyh.name/blog/entry/docker_run_debian/
[11]: https://wiki.debian.org/pt_BR/Debootstrap
[12]: http://blog.docker.com/2013/08/containers-docker-how-secure-are-they/
[13]: https://docs.docker.com/articles/security/
