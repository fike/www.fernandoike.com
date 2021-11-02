+++
title = "Observabilidade com OpenTelemetry"
date = 2021-11-02T20:37:16Z
draft = false
description = "O que é Observabilidade e OpenTelemetry"
tags = ["portugues", "opentelemetry", "kubernetes", "cncf"]
categories = ["portugues", "opentelemetry", "kubernetes", "cncf"]
+++

![tela do make menuconfig para compilar o kernel linux, a imagem original é da linux.com](/images/kernel_compile_1.jpg) 

Quem compila o Kernel do Linux em 2021?
 
Alguns, na verdade muitos, anos atrás era comum encontrar tutoriais de como compilar e atualizar o kernel do Linux num computador, as distribuições GNU/Linux não tinham um bom suporte para hardware na maioria dos computadores que eram usados naquela época. Com o passar dos anos a comunidade em torno dele evoluiu que dificilmente nos dias atuais tem alguma necessidade de compilar e instalá-lo.
 
Se você não vivenciou a grande aventura que era compilar e atualizar o Kernel mas quer saber como fazer, pode ler o [Guia Foca Linux](https://www.guiafoca.org/guiaonline/intermediario/ch16s11.html).
 
Como compilar o Kernel do Linux já não é tão comum, o mesmo pode-se dizer de gerenciar servidores físicos (bare metal) como naquele tempo. Também alguns anos atrás gerenciar a infraestrutura de virtualização foi teve grande destaque; gerenciar essa infraestrutura através de projetos como Xen, VMWare, etc. era comum. Atualmente, essa relevância está no Kubernetes, tanto em conteúdo técnico (textos, treinamentos, podcast, vídeos, etc) a ser consumido como certificações. Alguns anos atrás as certificações da LPI tinham destaque como parte do objetivos das pessoas que almejavam crescer na carreira, atualmente as referências são as certificações dos principais provedores de Cloud ou relacionadas ao Kubernetes (exemplo: CKA).
 
O [Daniel Requena](https://twitter.com/daniel_requena) faleu desse processo de evolução tencnológica numa apresentação chamada "[O poder das abstrações](https://speakerdeck.com/drequena/o-poder-da-abstracao)", a cada ciclo a evolução tecnologia cria novas camadas de fundação tecnológica, isso possibilita as pessoas de tecnologia não terem que passar horas ou dias lidando com gerenciamento de servidores de email (Sendmail, Postfix, Exim, etc.) ou passando horas compilando o Kernel Linux para habilitar o suporte da port [LPT1](https://en.wikipedia.org/wiki/Parallel_port).
 
Exercendo um pouco minhas habilidades de futurólogo (é uma ironia! 😉)... A administração do Kubernetes deve se tornar cada vez mais simples e um chute é de que CRDs se tornaram cada vez mais relevantes, mas sobre eles (CRDs) é para um outro texto. Observabilidade é um tema que está se tornando cada vez mais importante porque a arquitetura das aplicações está cada vez mais complexa e com dependências externas.
 
O intervalo de tempo (de menos de 1 hora) para restaurar serviço em [organizações do tipo Elite](https://cloud.google.com/blog/products/devops-sre/announcing-dora-2021-accelerate-state-of-devops-report) é mais fácil alcançar com a implementação de observabilidade. O "**caos organizado**" do crescimento (des)ordenado dos micro-serviços numa organização torna-se um desafio identificar com rapidez quais sãos os eventos importantes num incidente. O uso métricas, logs e traces torna possível saber o que realmente está acontecendo num fluxo de negócio que depende de vários micro-serviços.
 
# O que é Observabilidade?
 
A definição de observabilidade Honeycomb [num texto de 2017](https://www.honeycomb.io/blog/best-practices-for-observability/) é "*Um sistema é **observável** de forma que você pode explicar o que está acontecendo por dentro (de um sistema) apenas observando do lado de fora*". Para observar do lado de fora é necessário usar dados de telemetria como fazem as equipes de (corrida) veículos motores, eles coletam e interpretam os dados coletados para identificar eventuais problemas ou mudanças no acerto de um carro de corrida baseado nos dados. Assim como, acontece na indústria aeronáutica e espacial.
 
Traces, logs e métricas são a base da telemetria para nós tecnologias, assim como a telemetria é a base para a observabilidade. Mas quanto a telemetria pode facilitar a compreensão de um evento?
 
![imagem da telemetria do acidente do Maverick Viñales no GP da Estíria - imagem do site motogp.com](/images/telemetria_vinales_styria.jpg)
 
A [imagem](https://www.motogp.com/en/news/2020/08/26/analysis-and-data-as-vinales-dodged-disaster-in-austria/341765) acima é da telemetria da moto do Maverick Viñales, [os dados](https://www.motogp.com/en/news/2020/08/26/analysis-and-data-as-vinales-dodged-disaster-in-austria/341765) são do momento que ele caiu na corrida da MotoGP no GP da Estíria em 2020. Os dados da telemetria mostram que ele estava à **218 km/h** quando ele pulou da moto, os airbags da sua roupa foram abertos milissegundos antes dele cair no asfalto com impacto acima de **20G**. Ele deslizou por **4,8 segundos** até desacelerar após a queda por **1,9 segundos**.

Não é legal essa referência entre corridas e nosso trabalho como tecnologistas? A primeira vez que eu vi foi numa apresentação da [Tatiane Paya](https://www.linkedin.com/in/tatypaya) no (DevOpsDays Porto Alegre de 2019)[https://devopsdays.org/events/2019-porto-alegre/welcome/] no qual ela [falou sobre Arrancadas e DevOps](https://speakerdeck.com/tpaya/arrancada-o-que-este-esporte-pode-nos-ensinar-sobre-agilidade-e-performance).
  
Ah!!! Não é simplesmente instalar um agente de **A**pplication **P**erformance **M**onitoring, configurar alertas e criar alguns dashboards, há uma diferença simples mas importante segundo eles: "*Observabilidade é absolutamente, totalmente sobre instrumentação. O delta entre observabilidade e monitoramento é absolutamente as partes que são focadas em engenharia de software.*".
 
 
# O que é OpenTelemetry?
 
Segundo o próprio site do projeto, "*OpenTelemetry é um conjunto de APIs, SDKs, ferramentas e integrações que foram projetadas para a criação e gerenciamento de dados de telemetria como traces, métricas e logs. O projeto fornece uma implementação agnóstica de fornecedor que pode ser configurado para enviar dados de telemetria para o(s) backend(s) da sua escolha. Ele suporta uma variedade de projetos Open Source, incluindo Jaeger e Prometheus.*". Como ficam os projetos OpenCensus e o OpenTracing que também estão no guarda-chuva da [CNCF](https://www.cncf.io/)? O [OpenTelemetry](https://opentelemetry.io/) é a junção destes dois projetos, sendo que eles preteridos em favor do Otel (OpenTelemetry para os mais chegados).
 
Otel já tem suporte a diversas linguagens de programação e frameworks, ainda está maduro o suficiente em algumas partes mas isso deve-se resolver em breve pela quantidade de empresas envolvidas como Splunk, LightStep, HoneyComb, New Relic, etc. Se quiser o que o OpenTelemetry já suporta, dê uma olhada no [Registry](https://opentelemetry.io/registry/) do projeto.
 
A comunidade do OpenTelemetry é um das mais ativas da CNCF, no momento que vos escrevo é o segundo projeto [mais ativo](https://all.devstats.cncf.io/d/1/activity-repository-groups?orgId=1), ficando atrás somente do Kubernetes. Assim como Kubernetes se tornou o principal orquestrador de container, o OpenTelemetry deve se tornar o principal framework de observabilidade.
 
![](/images/otel_dev_stats.png)
 
Se quiser saber um pouco mais, [aqui](https://speakerdeck.com/fernandoike/observabilidade-com-opentelemetry) tem os slides da apresentação realizada no canal do Twitch do [LinuxTips](https://www.linuxtips.io/) (Valeu, [Jefferson](https://twitter.com/badtux_)!!!).
 
{{< speakerdeck 18bd484914304575950cdf0adeb792c5 >}}
 
Se quiser ver o vídeo da apresentação, está [aqui](https://www.twitch.tv/videos/1172147054).
 
{{< twitch 1172147054 >}}
 

Referências:
1 - [How to Compile a Linux Kernel](https://www.linux.com/topic/desktop/how-compile-linux-kernel-0/)
2 - [Analysis and data as Viñales dodged disaster in Austria](https://www.motogp.com/en/news/2020/08/26/analysis-and-data-as-vinales-dodged-disaster-in-austria/341765)
3 - [OpenTelemetry](https://opentelemetry.io/docs/)
4 - [Guia Foca Linux](https://www.guiafoca.org/guiaonline/intermediario/ch16s11.html)
5 - [Arrancada (DevOps)](https://speakerdeck.com/tpaya/arrancada-o-que-este-esporte-pode-nos-ensinar-sobre-agilidade-e-performance)
6 - [Best Practices for Observability](https://www.honeycomb.io/blog/best-practices-for-observability/)
7 - [Recompilando o Kernel](https://www.guiafoca.org/guiaonline/intermediario/ch16s11.html)