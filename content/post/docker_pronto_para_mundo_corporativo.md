+++
tags = ["portugues", "docker", "devops", "container", "linux", "aws", "azure "]
draft = false
date = "2017-03-30T18:57:01-03:00"
title = "Docker pronto para o mundo corporativo"
description = "Um resumo da mudança dos produtos da Docker"
categories = ["docker", "portugues"]

+++
![](/images/docker_lifecycle.png)

Um dos questionamentos que mais ouvi sobre [Docker](https://www.docker.com) em 2016 foi a falta de uma versão **LTS** (Long-Term Support). As empresas argumentavam que o ciclo frenético de versões do Docker gerava alguns transtornos para eles porque não conseguiam atualizar o Docker na mesma velocidade dos lançamentos das versões. Outro questionamento recorrente era que falta de retro compatibilidade da API das novas versões lançadas. No início de 2017 a Docker alterou o nome da **Docker Engine** para [Docker Community Edition](https://www.docker.com/community-edition) e a [Docker Engine CS (Commercially Supported)](https://docs.docker.com/cs-engine/1.13/) para [Docker Enterprise Edition](https://docs.docker.com/enterprise/).

Outro questionamento que ouvi bastante era como fazer para entregar software pago? Se fosse VM, bastava baixar a imagem e cadastrar a licença. Para isso foi criado o [Docker Store](https://docs.docker.com/docker-store/#get-an-image-from-the-docker-store), é um *markteplace* para imagem de containers, plugins, etc. Além da mudança de nome dos produtos, também foi alterado a lógica da numeração das versões.

### Community Edition

É a versão gratuita do Docker Engine, ela roda nas principais distribuições Linux ([Debian](https://www.debian.org/), [Ubuntu](https://www.ubuntu.com/), [CentOS](https://www.centos.org/) e [Fedora](https://getfedora.org/)), MacOSX, Windows 10 e na [AWS](https://aws.amazon.com/) e [Azure](https://azure.microsoft.com/). Ela tem uma versão de "desenvolvimento" chamada **Edge** e lançamento mensal, a estável (**stable**) terá novas versões a cada três meses. As versões agora são numeradas **ano.mês**: 17.03, 17.06, etc.


### Enterprise Edition

Versão paga do Docker, é tem mela também terá novas versões a cada três meses mas com suporte a bug fixes e correções de segurança por um ano. A numeração das versões segue a mesma lógica da versão estável da Community Edition. Ela roda no Ubuntu, Red Hat Enterprise Linux, CentOS, Oracle Linux, Suse Linux Enterprise Server, Microsoft Windows Server 2016, Azure e AWS (Amazon Web Services). Um outro diferencial da versão Enterprise Edition é a criação de certificação de serviços e produtos certificados como a maioria das empresas que oferecem serviços "Enterprise".

![](/images/docker_ee_lifecycle.png)
