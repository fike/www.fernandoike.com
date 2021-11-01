+++
title = "Observabilidade com OpenTelemetry"
date = 2021-11-01T00:37:16Z
draft = true
description = "O que é Observabilidade e OpenTelemetry"
tags = ["portugues", "opentelemetry", "kubernetes", "cncf"]
categories = ["portugues", "opentelemetry", "kubernetes", "cncf"]
+++

Quem compila o Kernel do Linux atualmente?

Alguns, na verdade muitos, anos atrás era comum encontrar tutoriais de como compilar e atualizar o kernel do Linux num computador, as distribuições GNU/Linux não tinham um bom suporte para hardware na maioria dos computadores que eram usados naquela época. Com o passar dos anos a comunidade em torno dele evoluiu que difícilmente nos dias atuais tem alguma necessidade de compilar e instalá-lo. 

Se você não vivenciou a grande aventura que era compilar e atualizar o Kernel mas quer saber como fazer, pode ler o [Guia Foca Linux](https://www.guiafoca.org/guiaonline/intermediario/ch16s11.html).

Como compilar o Kernel do Linux já não é tão comum, o mesmo pode-se dizer de gerenciar servidores físicos (bare metal) como naquele tempo. Também alguns anos atrás gerenciar a infraestrutura de virtualização foi teve grande destaque; gerenciar essa infraestrutura através de projetos como Xen, VMWare, etc. era comum. Atualmente, essa relevância está no Kubernetes, tanto em conteúdo técnico (textos, treinamentos, podcast, vídeos, etc) a ser consumido como certificações. Alguns anos atrás as certificações da LPI tinham destaque como parte do objetivos das pessoas que almejavam crescer na carreira, atualmente as referências são as certificações dos principais provedores de Cloud ou relacionadas ao Kubernetes (exemplo: CKA). 

O [Daniel Requena](https://twitter.com/daniel_requena) faleu desse processo de evolução tencnológica numa apresentação chamada "[O poder das abstrações](https://speakerdeck.com/drequena/o-poder-da-abstracao)", a cada ciclo a evolução tecnologia cria novas camadas de fundação tecnológica, isso possibilita as pessoas de tecnologia não terem que passar horas ou dias lidando com gerenciamento de servidores de email (Sendmail, Postfix, Exim, etc.) ou passando horas compilando o Kernel Linux para habilitar o suporte da port [LPT1](https://en.wikipedia.org/wiki/Parallel_port).

Exercendo um pouco minhas habilidades de futurólogo (é uma ironia! 😉)... Administração do Kubernetes deve se tornar cada vez mais simples e um chute é de que CRDs se tornaram cada vez mais relevante, mas sobre eles (CRDs) é para um outro texto. Observabilidade é um tema que está se tornando cada vez mais importante porque a arquitetura das aplicações está cada vez mais complexa e com dependências externas. 

O intervalo de tempo (de menos de 1 hora) para restaurar serviço em [organizações do tipo Elite](https://cloud.google.com/blog/products/devops-sre/announcing-dora-2021-accelerate-state-of-devops-report) é mais fácil alcançar com a implementação de observabilidade. O "caos organizado" do crescimento (des)ordenado dos micro-serviços numa organização torna-se um desafio identificar com rapidez quais sãos os eventos importantes num incidente, somente com o uso métricas, logs e traces é possível sabemos o que realmente está acontecendo num fluxo de negócio. 

Assim como Kubernetes se tornou o principal orquestrador de container, o OpenTelemetry deve se tornaro principal framework de observabilidade. Ele é [junção](https://www.cncf.io/blog/2019/05/21/a-brief-history-of-opentelemetry-so-far/) de dois projetos da CNCF: OpenCensus e OpenTracing; sendo, atualmente, (Outubro/2021) um dos projetos [mais ativos](https://all.devstats.cncf.io/d/1/activity-repository-groups?orgId=1) da CNCF.

![](/images/otel_dev_stats.png)

# O que é OpenTelemtry?

Segundo o próprio site do projeto, "*OpenTelemetry é um conjunto de APIs, SDKs, ferramentas e integrações que foram projetadas para a criação e gerenciamento de dados dde telemetria como traces, métricas e logs. O projeto fornece uma implementação agnóstica de fornecedor que pode ser configurado para enviar dados de telemetria para o(s) backend(s) da sua escolha. Ele suporta uma variedade de projetos OpenSource, incluindo Jeager e Prometheus.*".

Ele já tem suporte a diversas linguagens de programação e frameworks, ainda está maduro o suficiente em algumas partes mas isso deve-se resolver em breve pela quantidade de empresas envolvidas como Splunk, LightStep, HoneyComb, New Relic, etc. Se quiser saber mais, dê uma olhada no [Registry](https://opentelemetry.io/registry/) do projeto.

Se quiser saber um pouco mais, [aqui](https://speakerdeck.com/fernandoike/observabilidade-com-opentelemetry) tem os slides da apresentação realizada no canal do Twitch do LinuxTips (Valeu, Jefferson!!!).

{{< speakerdeck 18bd484914304575950cdf0adeb792c5 >}}

Se quiser ver o vídeo da apresentação, está [aqui](https://www.twitch.tv/videos/1172147054).

{{< twitch 1172147054 >}}
