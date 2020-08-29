+++
title = "Instalando Docker CE no Debian"
description = "Instalação do Docker Community Edition 17.03 no CentOS"
categories = ["devops", "docker", "portugues"]
tags = ["portugues", "docker", "devops", "linux", "centos", "systemd"]
draft = false
date = "2017-04-03T12:28:50-03:00"

+++
A Docker mudou o nome dos seus produtos e o *Docker Engine* agora é conhecido como **C**ommunity **E**dition. Se ainda não leu a respeito, você pode ler pequeno resumo que escrevi sobre a mudança no "*[Docker pronto para o mundo corporativo](https://www.fernandoike.com.br/2017/03/30/docker-pronto-para-o-mundo-corporativo/)*". Uma outra mudança para fazer a instalação a instalação mudou, para instalar as versões anteriores era usado o **packages.docker.com** e a partir da versão 17.03 o repositório é **download.docker.com**.

Este mini tutorial usa como base o [Debian Jessie](https://www.debian.org/releases/jessie/) e é ligeiramente modificado do roteiro de instalação da [documentação oficial](https://docs.docker.com/engine/installation/linux/centos/) do Docker CE Stable. Há uma outra pequena diferença é que aqui foi usado o usuário *root* e também a instalação de um arquivo adicional da configuração do Docker no [Systemd](https://www.freedesktop.org/wiki/Software/systemd/).


## Removendo versões anteriores

Se houver um repositório Docker já configurado, lembre-se de remover ele e também o pacote docker que não seja do repositório da Docker e suas dependências. Exemplo: O pacote Docker encontrado no Debian é **docker.io**
```
#apt-get remove docker.io
```

## Configurando o repositório

O repositório da Docker usa HTTPS e para usá-lo é necessário adicionar o pacote **apt-transport-https**, o **software-properties-common** permite gerenciar os repositórios sem ter editar manualmente os arquivos.
```
#apt-get update

#apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl \
  software-properties-common
```

Baixando a chave GPG do repositório Docker e adicionando o repositório .
```
#curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

#add-apt-repository \
         "deb [arch=amd64] https://download.docker.com/linux/debian \
         $(lsb_release -cs) \
         stable"
```

Instalando o pacote Docker Community Edition.
```
#apt-get update

#apt-get -y install docker-ce
```

A versão kernel Linux padrão da Jessie é bem antigo (3.16), se quiser usar uma versão mais recente poderá instalar via [Backports](https://backports.debian.org/). No momento em que este mini tutorial estava sendo escrito a versão mais atual disponível era 4.9, nesta versão foi removido o patch do AUFS e não tem uma versão do módulo dele no Backports para instalar. Portanto, para usar o Docker com um kernel Linux recente terá que modificar os parâmetros de inicialização do serviço Docker no Systemd para usar outro sistema de arquivo como OverlayFS.

Como no "[Instalando Docker CE no CentOS](https://www.fernandoike.com.br/2017/04/02/instalando-docker-ce-no-centos/)", a recomendação é usar o diretório "**/etc/systemd/system/**" para usar os parâmetros específicos da inicialização do Docker via Systemd. Um detalhe diferente da instalação no CentOS é que se modificar o "/etc/default/docker" não terá nenhum efeito se o boot for com o Systemd, ele só tem efeito para o Debian que usa como boot Sysvinit/Upstart.

Criar o diretório "**docker.service.d**"".
```
#mkdir -p /etc/systemd/system/docker.service.d/
```

Criar o arquivo environment.conf via linha de comando.
```
#cat << EOF >> /etc/systemd/system/docker.service.d/environment.conf
[Service]
EnvironmentFile=/etc/default/docker
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// $DOCKER_OPTS
EOF
```

Fazer o Systemd reconhecer a alteração
```
#systemctl daemon-reload
```

Adicionar o repositório Backports e atualizar a lista de pacotes.
```
#add-apt-repository \
        "deb http://ftp.debian.org/debian jessie-backports main"

#apt-get update
```

Instalar a versão 4.9 do Kernel Linux
```
#apt-get -t jessie-backports install linux-image-4.9.0-0.bpo.2-amd64
```

Editar o /etc/default/docker para trocar o sistema de arquivo para OverlayFS
```
#vim /etc/default/docker
[...]
DOCKER_OPTS="-s overlay2"
[...]
```

Reiniciar para usar o Kernel Linux mais recente.
```
#reboot
```

Após o boot, ao rodar o docker info deverá ter a saída parecida como está abaixo.
```
#docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 17.03.1-ce
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
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
Kernel Version: 4.9.0-0.bpo.2-amd64
Operating System: Debian GNU/Linux 8 (jessie)
OSType: linux
Architecture: x86_64
CPUs: 2
Total Memory: 492.4 MiB
Name: jessie
ID: F7WN:UTXT:Q2FT:ZDRA:OWEB:OQVN:KE6Y:43HP:76YF:HTDY:EGRZ:H76Q
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
WARNING: No swap limit support
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
```
