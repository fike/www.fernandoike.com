+++
title = "É o Futuro"
date = 2017-11-13T22:30:53-02:00
draft = false
description = "Tradução do texto de Paul Biggar (um dos fundadores da CircleCI) - It's future"
categories = ["portugues", "devops"]
tags = ["portugues", "devops", "containers", "circleci", "kubernetes", "docker"]
+++
![](/images/bunny.jpg)

[Paul Biggar](https://twitter.com/paulbiggar) ([@paulbiggar](https://twitter.com/paulbiggar)) escreveu no blog da [CircleCI](https://circleci.com/) uma pequena história sobre uma pessoa que desenvolveu um pequeno app (clássico CRUD) e outra pessoa é entusiasta das novas tecnologias. Abaixo uma tradução livre e o original está [aqui](https://circleci.com/blog/its-the-future/). Se achar qualquer erro na tradução ou no português, abra uma [issue](https://github.com/fike/www.fernandoike.com).

---

Oi, meu chefe disse para falar contigo - Soube que você manja muito sobre aplicações web?

**- Claro, Estou mais para um cara de sistemas distribuídos. Acabei de voltar da ContainerCamp e GlueCon, vou para a DockerCon na próxima semana. Estou muito empolgado em participar com a forma em que a indústria está se movendo - tornando tudo mais simples e confiável. É o futuro!**

Legal. Estou construindo uma aplicação web simples no momento - uma típica aplicação CRUD usando Rails e vai rodar no Heroku. É ainda o caminho a fazer?

**- Não, Isso é old school (antigo). Heroku está morto - ninguém usa mais. Você tem que usar Docker agora. É o futuro.**

Hm. Ok. O que é isso?

**- Docker é a nova forma de construir conteinerização. É como LXC, mas é também um formato de pacote, uma plataforma de distribuição (de apps) e ferramentas para fazer sistemas distribuídos realmente simples.**

Contain... - O que? O que é LXE?

**- É LXC. É um chroot com esteroides!**

O que é cher-oot?

**- Hum, veja. Docker. Conteinerização. É o futuro. É como virtualização mas rápido e barato.**

Ah, tipo Vagrant.

**- Não, Vagrant está morto. Tudo está indo para ser conteinerizado. É o futuro.**

Ok, não preciso saber mais nada sobre virtualização?

**- Não, você ainda precisa da virtualização porque contêineres não fornecem segurança completa ainda. Então, se você quer rodar qualquer coisa num ambiente multi-tenant, precisa garantir que nada escape do sandbox.**

Ok, me perdi um pouco no assunto. Vamos recapitular. Há uma coisa do tipo virtualização chamada contêineres. Posso usar isso no Heroku?

**- Veja bem, Heroku tem algum suporte ao docker mas como disse a você: Heroku está morto. Você precisa rodar seus containers no CoreOS.**

Hm. O que é isso?

**- É um ótimo Sistema Operacional que você pode usar como base para o Docker. Ah, você nem mesmo precisa do Docker, você pode usar rkt.**

Rocket?

**- Não, rkt.**

Certo, Rocket.

**- Não, é chamado de rkt. Totalmente diferente. É um formato alternativo de conteinerização que não é um bundle como docker e é mais modular.**

Isso é bom?

**- Claro que sim. Modularização é o futuro.**

Ok, como você usa isso?

**- Eu não sei. Eu acho que ninguém usa.**

Suspiro. Você pode dizer alguma coisa sobre o CoreOS?

**- Sim, é um sistema operacional que você usa com o Docker.**

O que é um Sistema Operacional hospedeiro (Host)?

**- Um Sistema Operacional que executa todos seus contêineres.**

Executa meus contêineres?

**- Claro, você tem que ter alguma coisa rodando seus contêineres. Então, você configura como uma instância EC2, coloca o CoreOS nele, executa o daemon do Docker e então faz o deploy das imagens Docker.**

Qual parte disso é o contêiner?

**- Tudo isso, Veja, você pega sua aplicação, escreve um Dockerfile, transforma em uma imagem local, então pode mandar para qualquer servidor Docker.**

Ah, como Heroku?

**- Não como Heroku. Como disse, Heroku está morto. Você pode rodar sua própria nuvem usando Docker.**

O que?

**Sim, é superfácil. Veja #gifee.**

Gify?

**- "Google's infraestructure for everyone" (Infraestrutura do Google para todos). Você pega algumas ferramentas e stacks usando contêineres e pode ter uma infraestrutura como tem o Google.**

Por que eu não só uso as coisas do Google?

**- Você acha que isso vai acontecer nos próximos 6 meses?**

Ok. Alguém já faz hospedagem desse tipo de coisa? Eu não quero hospedar por minha conta.

**- Bem, Amazon tem ECS mas você terá que escrever em XML ou alguma porcaria do tipo.**

E quanto a hospedagem de   alguma coisa no OpenStack?

**- Putz**

Putz?

**- Putz.**

Veja, eu realmente não quero hospedar por minha conta.

**- Não, é superfácil. Só configurar um cluster de Kubernetes.**

Eu preciso de um cluster?

**- Cluster de Kubernetes. Ele gerenciará os deploys de todos os serviços.**

Eu só tem um serviço.

**- O que quer dizer? Tem um app, certo? Você terá ao menos de 8 à 12 serviços?**

O que? Não, só um app. Serviço, tanto faz, Só um deles.

**- Não, olhe para micro serviços. É o futuro. É como fazemos tudo agora. Você pega seu app monolítico e divide em 12 serviços. Um para cada tarefa.**

Isso parece um exagero.

**É o único caminho para ser confiável. Então, se seu serviço de autenticação cair...**

Serviço de autenticação? I só queria usar esta gem que já use algumas vezes.

**- Legal. Use a gem. Coloque-o num projeto próprio. Crie uma API RESTful para ele. Em seguida, seus outros serviços usarão esta API e gerenciarão graciosamente as falhas. Coloque num contêiner e entregue continuamente esta porcaria.**

Ok, agora tenho dúzias de serviços não gerenciáveis. O que vem agora?

**- Bom, como disse sobre Kubernetes. Você orquestra todos os seus serviços.**

Orquestrar eles?

**Então, você tem esses serviços e precisa de múltiplas cópias deles para serem confiáveis. Kubernetes garante que você tenha o suficiente e que sejam distribuídos por vários servidores em seu cluster, por isso está sempre disponível.**

Eu preciso de um cluster agora?

**- Claro, pela confiabilidade. Mas Kubernetes gerencia isso e você sabe que o Kubernetes funciona por que o Google  construiu-o e roda no etcd.**

O que é etcd?

**- É uma implementação do RAFT?**

Ok, o que é Raft?

**- É como Paxos.**

Cristo. Indo a fundo neste maldito buraco de coelho em que estamos entrando. Só quero lançar um app. Suspiro. Ok, respira fundo. Jesus. Ok, o que é Paxos?

**- Paxos é como este protocolo de consenso distribuído muito antigo dos anos 70 que ninguém usa ou entende.**

Legal, obrigado por falar sobre eles. E Raft é o que?

**- Como ninguém entende o Paxos, este cara é o Diego...**

Ah, você conhece ele?

**- Não, ele trabalha na CoreOS. De qualquer forma, Diego construiu o Raft para sua tese de PhD porque Paxos era muito difícil. Um cara muito inteligente e doidão. Então, ele escreveu o ETCD como uma implementação e Aphyr disse que não é ruim.**

Quem é Aphyr?

**- Aphyr é o cara que escreveu, 'Call Me Maybe'. Você sabe, o sistema distribuído e o cara do BDSM?**

Hã? Você disse BDSM?

**- Sim, BDSM, é de São Francisco. Todos estão em sistemas distribuídos e BDSM.**

Ah, ok. Ele escreveu aquela música da Katy Perry?

**- Não, ele escreveu uma série de post sobre como todo banco de dados falha no CAP.**

O que é CAP?

**- O teorema CAP. Ele diz que você só pode ter dois das três: Consistência (Consistency), Disponibilidade (Disponibilidade) e Partição (Partition tolence).**

Ok, todos os bancos de dados falha com o CAP. O que isso quer dizer?

**- Isso significa que eles não prestam. Como o mongo.**

Pensei que o Mongo fazia web scale?

**- Ninguém mais fez.**

Ok, e o etcd?

**- Sim, etcd é um armazenamento chave-valor distribuído.**

Ah, como Redis.

**- Não, não como Redis. etcd é distribuído. Redis perde metade das escritas se tive partições de rede.**

Ok. Então é armazenamento chave-valor **distribuído**. No que ele é útil?

**- Kubernetes configura um cluster padrão de 5 nós usando etcd como um barramento de mensagens. Ele combina com alguns dos serviços próprios do Kubernetes para fornecer um sistema de orquestração muito resiliente.**

5 nós? Eu tenho um app. Quantas máquinas vou precisar para tudo isso?

**- Bem, terá cerca 12 serviços, e claro, você precisará de algumas cópias de cada um, alguns balanceadores de carga, o cluster do etcd, seu banco de dados e o cluster do kubernetes. Portanto, seria como se 50 contêineres em execução.**

PQP!

**- Nada demais! Containers são realmente eficientes, você poderia distribuir eles por 8 máquinas! Não é incrível?**

Esse é um jeito de fazer. Serei capaz de fazer um simples deploy do meu app com tudo isso?

**- Claro, armazenamento (storage) é uma questão em aberto com Docker e Kubernetes e rede dá um pouco de trabalho mas o básico está lá.**

Ok, Entendo. Acho que consigo.

**- Legal.**

Obrigado por explicar.

**- De nada**

Deixe só eu resumir para ver se entendi direito.

**- Claro.**

Então, só preciso separar meu app CRUD em 12 micro-serviços, cada com sua própria API na qual chama outras APIs mas tolerante a falhas, coloco dentro de contêineres Docker, instalo um cluster de 8 máquinas que terão Docker Host rodando CoreOS, “orquestrador” deles usando um pequeno cluster de Kubernetes rodando etcd, entendendo as “questões abertas” de rede e armazenamento e então entrego continuamente múltiplas cópias redundantes de cada micro-serviço no meu cluster. É isso?

**Sim! Não é glorioso?**

Vou voltar para o Heroku.
