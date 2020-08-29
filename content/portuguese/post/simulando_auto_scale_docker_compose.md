+++
title = "Simulando Auto Scale com Docker Compose"
date = 2019-03-02T18:50:43-03:00
draft = false
description = "Uma tutorial do zero até simular Auto-Scale usando Docker e Docker Compose"
categories = ["docker", "portugues", "devops", "containers"]
tags = ["docker", "docker-compose", "kubernetes", "containers"]
+++

Este post é baseado num workshop ministrado numa das empresas que trabalhei e na Campus Party São Paulo 2019, ele irá fazer o básico até o uma simulação de auto-scale usando o Docker Composer. Aí, vem a pergunta, por que?

Para observar o comportamento da aplicação se funciona num cenário de auto-scale de usando um orquestrador de containers como Kubernetes, DC/OS ou Docker Swarm antes da funcionalidade ir para o repositório do projeto no qual está trabalhando. 

## Requisitos 

* [Docker](https://docs.docker.com/engine/) 
* [Docker Compose](https://docs.docker.com/compose/)
* [Traefik](https://traefik.io/)
* [Redis](https://redis.io/)
* [Flask](https://flask.pocoo.org/)


## Docker 101

Há duas formas de seguir este tutorial: instalando no computador ou via Play-with-Docker.

1. A instalação do Docker pode ser os passos do livro [Docker para Desenvolvedores](https://leanpub.com/dockerparadesenvolvedores) do [@Gomex](https://twitter.com/gomex)

2. Abra o Play-With-Docker ou use Docker instalado no seu computador. Necessário ter uma conta na docker.

- [https://labs.play-with-docker.com/](https://labs.play-with-docker.com/)
- [Para abrir uma conta no Docker](https://hub.docker.com/signup?next=%2F%3Fref%3Dlogin)

3. Clonar o repositório Git do workshop

        $ git clone https://github.com/fike/docker-workshop.git
        $ cd docker-workshop

4. O Docker gera as imagens de containers através das instruções contidas no [Dockerfile](https://docs.docker.com/engine/reference/builder/). Para criar uma image usando Dockerfile usa-se o comando `docker build`. O `-t` é para definir o nome da imagem (tag).
    
        $ docker build -t hello .

    **Bônus**: uma leitura posterior é recomendada no "[Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)"

5. A imagem será criada no computador onde foi executado o `docker build`, as imagens em cache/armazenadas podem ser visualizadas usando o comando abaixo:

        $ docker images
        REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
        hello               latest              5877ef9de68e        About a minute ago   196MB

    Perceba que a imagem é gerada por padrão com a tag `latest`.

6. Se quiser gerar novamente uma imagem e manter a anterior com o mesmo nome, pode-se definir uma tag no momento da geração da imagem.

        $ docker build -t hello:1 .

    **Bônus**: uma boa prática recomendada para gerenciar versão da imagem, mantenedor da imagem e qualquer outras informações (metadados); recomenda-se usar o `LABEL` no Dockerfile ou usar o parâmetro `--label`:

        Gera a imagem com diversos label
        $ docker build -t hello:2 --label app=hello --label MAINTAINER="Foo bar <foo@bar.com>"  --label build=1 .

        $ docker inspect -f '{{index .ContainerConfig.Labels}}' hello:2
        map[MAINTAINER:Foo bar <foo@bar.com> app:hello build:1]

        $ docker inspect -f '{{index .ContainerConfig.Labels "app"}}' hello:2
        hello
     
7. Para acessar uma porta dentro de um container é necessário passar para o Docker quais portas serão expostas. O app do workshop roda na porta 80/TCP, para acessar essa porta é necessário dizer para o Docker qual porta externa será mapeada. O mapeamento de porta é dado por `-p PORTA_EXTERNA:PORTA_INTERNA`.

    O parâmetro `-d` faz com que o container rode no _background_.

        $ docker run -d -p 4000:80 hello

    O site estará disponível via `https://localhost:4000`, se você executou o comando em seu computador, ou em um pequeno link no **play-with-docker** com o número 4000.

    ***

    ![image](https://user-images.githubusercontent.com/7269710/31366135-e58a108a-ad45-11e7-8298-e1255ab8e311.png)

    ***

    ![image](https://user-images.githubusercontent.com/7269710/31366181-22af61ae-ad46-11e7-9b99-fec4efa8a04c.png)

    ***

O Hello World do app deste workshop usa o [Redis](https://redis.io/) para contar os acessos (como não subimos o Redis, o contador está desativado!). Mas antes de subir o Redis é necessário criar uma rede na qual será feita a comunicação entre o app e ele:

8. Criar a rede _workshop_

        $ docker network create workshop

9. A rede criada, é só rodar o container do Redis e do App na mesma rede. Não se esqueça de finalizar o container anterior que está no _background_!
    
        Finalizar o container do app
        $ docker stop $(docker ps | grep hello | awk '{ print $1 }')
    
        Executando o Redis
        $ docker run -d --name redis --network workshop redis
    
        Executando o app
        $ docker run -d --name hello --network workshop -p 4000:80 hello

10. Como no passo 5, abra no browser a URL https://localhost:4000/ ou clique no **4000** se estiver usando o Play-With-Docker. Faça o reload algumas vezes, contador irá funcionar desta vez. 

11. Compartilhando volumes (_stateful cases_). O Docker possibilita compartilhar volumes entre containers de forma bastante simples:

        Criando volume
        $ docker volume create workshop_data
    
        Lista os volumes criados
        $ docker volume ls

12. Vamos agora iniciar um container com acesso ao volume compartilhado. O mapeamento de volume é dado por `-v VOLUME_HOST:VOLUME_CONTAINER`.
  
  
    > VOLUME_CONTAINER é o path que o volume será montado no container

    
    Os parâmetros `-it` conectam seu terminal com um terminal _dentro_ do contêiner.

        Executar um container e criar um arquivo com alguma informação
        $ docker run -it -v workshop_data:/storage debian bash
        $ echo "Oi, consegue ler?" > /storage/README
        $ exit
 
13. O container no passo anterior criou um arquivo em '/storage' como o nome README. Acrescente mais uma informação executando outro container:

        $ docker run -it -v workshop_data:/storage debian bash
        $ cat /storage/README
        $ echo "Sim, consigo ler!" >> /storage/README
        $ exit

    **Extra**: Como compartilhar um diretório do host com o container? 

## Docker Compose

O Docker Compose facilita a comunicação de entre containers para fazer testes ou em desenvolvimento de aplicações (não deve ser usado em ambientes de produção). No diretório do workshop há um arquivo `docker-compose.yml` no qual tem as informações para subir o app deste workshop e o Redis.
    
1. Gerando as imagens:  

        Parar todos os containers
        $ docker stop $(docker ps -aq)
        
        $ docker-compose build

2. Como o Docker (comando), o Docker Compose também tem o argumento **ps** para listar os containers.

        Rodar os containers no background
        $ docker-compose up -d
    
        Listar o containers em execução
        $ docker-compose ps

Você pode abrir novamente o browser `https://localhost:4000/` ou clicar no **4000** se estiver usando o **play-with-docker**. Note que o contador reniciou.

3. Finalize os containers em execução:

        $ docker-compose stop

A "inteligência" para reconhecer as novas instâncias do app hello-world é o Traefik acessar o a API Docker para identificar novas instacias nada rede na qual ele está em execução. Assim, pode simular o comportamento em produção de uma aplicação ao fazer o *up scale* e o *down scale*.

## Auto-Scaling


1.  Subindo o app e Redis via Docker Compose. Após a execução do Docker Compose, o app estará disponível da mesma fora mencionado (`https://localhost:4000`). Abra o browser novamente e recarregue algumas vezes, observe que o hostname não varia.

        Gerando as imagens
        $ docker-compose -f docker-compose-scale.yml build

        Executando os containers
        $ docker-compose -f docker-compose-scale.yml up -d  

2.  O arquivo de configuração `docker-compose-scale.yml` tem dois serviços: `hello` e `redis`. O  comando abaixo irá aumenta o número de containers de `hello` para 5:
    
        $ docker-compose -f docker-compose-scale.yml up -d --scale hello=5

Abra o browser novamente em `https://localhost:4000/` e recarregue a página algumas vezes. O hostname deverá ser diferente toda vez que abrir a página, isso porque a cada requisição o Traefik está enviando a requisição para um container.

## Extra: Mais Comandos

17. Alguns comandos avançados:

        Adquire informações detalhadas sobre um object Docker
        $ docker inspect

        Remove objetos Docker não usados (containers, imagens, redes e volumes)
        $ docker system prune

        Remove apenas os containers parados
        $ docker rm $(docker ps -aq -f status=exited)

        Compila uma aplicação Go
        $ docker run  --rm -v "$PWD":/d/helloworld -w /d/helloworld golang go build helloworld.go

## Extra: Docker Registry

Acesse https://hub.docker.com, lá você encontra uma biblioteca de inúmeras imagens Docker!

Crie uma conta no site, e você pode agora publicar suas próprias imagens! Todas as imagens são nomeadas seguindo o padrão `repositorio/imagem:tag`; `repositorio` corresponde ao id de sua conta ou de sua organização (por exemplo, https://hub.docker.com/r/maburix).

Para publicar uma imagem, troque o tag de uma imagem para seguir a convenção, e então utilize `docker push`:

         $ docker tag hello <nome-de-sua-conta>/hello
         $ docker push <nome-de-sua-conta>/hello

Agora todo o mundo pode baixar e rodar sua imagem!

         $ docker pull <nome-de-sua-conta>/hello


## Conclusão

**Auto-scale** é relativamente simples mas envolve muito componentes que estão relacionado a conceitos como [Infraestrutura Imutável](https://www.oreilly.com/ideas/an-introduction-to-immutable-infrastructure), 
[Orquestração de Containers](https://www.exoscale.com/syslog/container-orchestration/), [Continuous Delivery](https://continuousdelivery.com/), [Blue-Green Deployment](https://martinfowler.com/bliki/BlueGreenDeployment.html), [Canary Release](https://martinfowler.com/bliki/CanaryRelease.html), [Aplicações Stateless](https://www.contino.io/insights/stateless-vs-stateful-containers-whats-the-difference-and-why-does-it-matter), etc.
