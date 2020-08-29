+++
date = "2017-04-02T09:28:40-03:00"
title = "Instalando Docker CE no CentOS"
description = "Instalação do Docker Community Edition 17.03 no CentOS"
categories = ["devops", "docker", "portugues"]
tags = ["portugues", "docker", "devops", "linux", "centos", "systemd"]
draft = false

+++
A Docker mudou o nome dos seus produtos e o *Docker Engine* agora é conhecido como **C**ommunity **E**dition. Se ainda não leu a respeito, você pode ler pequeno resumo que escrevi sobre a mudança no "*[Docker pronto para o mundo corporativo](https://www.fernandoike.com.br/2017/03/30/docker-pronto-para-o-mundo-corporativo/)*". Uma outra mudança para fazer a instalação a instalação mudou, para instalar as versões anteriores era usado o **packages.docker.com** e a partir da versão 17.03 o repositório é **download.docker.com**.

Este mini tutorial usa como base o [CentOS](https://www.centos.org) 7 e é ligeiramente modificado do roteiro de instalação da [documentação oficial](https://docs.docker.com/engine/installation/linux/centos/) do Docker CE Stable. Há uma outra pequena diferença é que aqui foi usado o usuário *root* e também a instalação de um arquivo adicional da configuração do Docker no [Systemd](https://www.freedesktop.org/wiki/Software/systemd/).

## Removendo versões anteriores

Se houver um repositório Docker já configurado, lembre-se de remover ele e também o pacote docker que não seja do repositório da Docker (exemplo: repositório do CentOS) e suas dependências.
```
#yum remove docker \
                  docker-common \
                  container-selinux \
                  docker-selinux \
                  docker-engine
```

## Configurando o repositório

Instale o yum-utils, ele fornecerá o comando yum-config-manager para adicionar o repositório do Docker.
```
#yum install -y yum-utils
```

Adicione o repositório Docker usando o yum-config-manager.
```
#yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

## Instalando o Docker CE

Atualize o índice de pacotes e instale o pacote do Docker CE.
```
#yum makecache fast

#yum install docker-ce.x86_64
```

Configure para o Docker subir como serviço ao servidor iniciar.
```
#chkconfig docker on
```

Iniciando o serviço do Docker.
```
#systemctl start docker
```

## Bônus: Alterando do jeito certo o Docker no Systemd

Para adicionar ou alterar algum parâmetro de inicialização Docker via Systemd, alguns tutoriais dizem para alterar o arquivo **docker.service** nos diretórios "**/usr/lib/systemd/system**" ou "**/lib/systemd/system**". Minha sugestão é fazer isso em outro local, porque numa eventual uma atualização do pacote do Docker, o arquivo pode ser sobrescrito e você perder as alterações feitas para iniciar o serviço do Docker. Exemplo: "**/etc/systemd/system/**"

Criar o diretório "**docker.service.d**"".
```
#mkdir -p /etc/systemd/system/docker.service.d/
```

Criar o arquivo environment.conf via linha de comando.
```
#cat << EOF >> /etc/systemd/system/docker.service.d/environment.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H unix:///var/run/docker.sock
EOF
```

Fazer o Systemd reconhecer a alteração e reiniciando o serviço do Docker.
```
#systemctl daemon-reload

#systemctl restart docker
```

Para verificar as informações de instalação use o ```docker info```, o retorno deverá ser similar ao abaixo.
```
# docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 17.03.1-ce
Storage Driver: overlay
 Backing Filesystem: xfs
 Supports d_type: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 4ab9917febca54791c5f071a9d1f404867857fcc
runc version: 54296cf40ad8143b62dbcaa1d90e520a2136ddfe
init version: 949e6fa
Security Options:
 seccomp
  Profile: default
Kernel Version: 3.10.0-514.6.2.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 488.7 MiB
Name: localhost.localdomain
ID: NHOU:FKCN:547X:QTZU:IO23:YVOC:6WF5:2WEL:EXZ4:WFZQ:SCHH:YTQR
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
```
