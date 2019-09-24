+++
title = "Kanban, WIP e observações antropológicas"
date = 2019-09-24T10:44:13-03:00
draft = false
description = "O segundo caso de implantação de Kanban"
categories = ["kanban", "agile", "devops", "portugues"]
tags = ["kanban", "agile", "devops", "portugues", "scrum", "wip"]
+++
Algum tempo atrás postei no twitter uma referência sobre limitação de WIP (Work-in-Progress) e como isso impacta as mudanças nas equipes.

<blockquote class="twitter-tweet"><p lang="pt" dir="ltr">Não tenho certeza de quem ouvi mas acho que foi do <a href="https://twitter.com/rodrigoy?ref_src=twsrc%5Etfw">@rodrigoy</a>, não usando as mesmas palavras: Aplicar WIP no Kanban é uma experiência antropoĺógica. <a href="https://t.co/DrDZWi5uAY">pic.twitter.com/DrDZWi5uAY</a></p>&mdash; fernandoike (@fernandoike) <a href="https://twitter.com/fernandoike/status/1137056112996470785?ref_src=twsrc%5Etfw">June 7, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 


O tweet está relacionado a uma implantação do Kanban numa startup no qual a equipe de Engenharia, também conhecida como Tecnologia da Informação, estava mudando a forma de organizar suas atividades vindo de uma experiência anterior com Scrum. Idealmente esta implementação deveria ser baseada no [STATIK](), mas infelizmente não consegui seguir nessa linha. A experiência anterior das equipes com SCRUM possibilitou ter alguma organização dos projetos e atividades das equipes, mas havia um conflito constante entre o que estava sendo entregue pelas equipes e o que estava sendo demandado pelas outras das áreas da organização e clientes.

Havia dois problemas mais evidentes:

1 - Papéis demais para um mesmo responsável
Uma mesma pessoa exercia o papel de Scrum Master, Product Owner e ainda liderança das equipes (Scrum-Product-Boss). A sobreposição de papéis acabava, invariavelmente, numa comunicação verticalizada das equipes. Os desenvolvedores apenas executava as tarefas já previamente discriminadas pelo SPB, uma parte significativa dos desenvolvedores não sentiam-se responsáveis pelo desenvolvimento e pelas entregas previstas, eles se sentiam como Macaco Programadores. Como consequência, a maioria das novas funcionalidades, como também, correção de bugs eram entregues fora dos prazos estipulado.

Quando as pessoas que são responsáveis, neste caso os desenvolvedores, não têm a oportunidade de entender o contexto do projeto ou da atividade que está sendo designada para ele, o resultado quase sempre é o artefato que será entregue não corresponde ao que foi requisitado.

2 - A inflexibilidade dos rituais
Qualquer framework que muda o modo a forma de trabalhar deve respeitar a cultura organizacional vigente. Respeitar no sentido de entender o contexto no qual está sendo aplicado o framework, implementa de forma abrupta leva um tensionamento entre as pessoas não importando qual o papel que cada um exerce. Seja um ERP, um método relacionado a Agilidade ou qualquer outro.

O planejamento e backlog seguiam o ritual de enquanto não entregar a atividade em andamento, não se adiciona nada no backlog. Mesmo quando havia priorização pela liderança da organização como uma oportunidade de novos negócios ou uma urgência solicitada por um cliente. Isso gerava um tensão e insegurança se realmente conseguiriam entregar o que estava acordado com os clientes.

O problema aqui não é que o Scrum não funciona, mas sim de que a organização não estava com o nível de maturidade para organizar as equipes, bem como, os projetos com papéis bem definidos para aplicá-lo


## A aplicação do Kanban

Como havia muita resistência em mudanças devido a implantação anterior (Scrum), a estratégia adotada para implantar o Kanban foi implementar gradualmente e de forma evolutiva. Antes de adotá-lo mudou-se a maneira de como as equipes estavam organizadas, a mudança foi orientada ao direcionamento que as lideranças da organização planejaram para o próximo período. Inicialmente, o quadro tinha apenas uma classe de serviço. A motivação era ter a visão de que todo mundo estava fazendo, identificar as dificuldades que estavam enfrentando para a conclusão das atividades demandadas.

Funcionou muito bem no início no sentido de transparência e visualização, claro que não esta organização do quadro Kanban não era eficiente. As pessoas perdiam um tempo para encontrar as suas atividades e logo iniciaram uma discussão de mudar o layout. A segunda versão já contava com três Classe de Serviços, uma para cada equipe e uma terceira para projetos e tarefas relacionadas a Infraestrutura de TI.

Esta nova organização melhorou as reuniões diárias de cada equipe, contudo as pessoas moviam os cartões para executar a atividade mas as atividades não eram finalizadas no Kanban. Isso representava a realidade, para os desenvolvedores o conceito de finalizado era de realizar o commit no repositório Git na árvore principal. Contudo, isso não era realmente o conceito que a organização entendia como finalizado, para organização "finalizado" significava que a funcionalidade desenvolvida foi validada por testes manuais e/ou automáticos, como também, instalada em produção.

**Cumulative Flow Diagram da implantação inicial do Kanban**
![CFD antes de aplicar WIP](/images/CumulativeFlowDiagram.png)

Apesar desta diferença no entendimento da definição de finalizado, já havia efeito positivo na organização: as funcionalidades, correções de bugs estavam alinhado com a expectativa da liderança da organização e clientes. Qualquer um poderia olhar o que estava em andamento, em qual etapa estava uma funcionalidade específica, dar um novo direcionamento para uma tarefa se houvesse necessidade.

# Aplicação do WIP

Diuturnamente era conversado com as equipes para "cuidar" da funcionalidade até que ela fosse instalada em produção. Conforme a funcionalidade desenvolvida fosse avançado no pipeline do serviço de Continuous Delivery, a pessoa responsável pela funcionalidade deveria mover o cartão para os respectivo estágio do pipeline no Kanban. A adoção desta política não foi muito efetiva até implantar WIP em cada etapa do pipeline.

Cada equipe estabeleceu o tamanho do WIP em cada estágio do Pipeline, se o limite do WIP fosse ultrapassado em um estágio, deveria ser justificar a inclusão de um novo cartão naquele estágio. Junto com o insistência nas reuniões diárias sobre qual a definição de **finalizado** para organização, contribuiu muito para não se acumulasse cartões em algum estágio. Ou seja, as tarefas não mais ficavam mais acumuladas, por exemplo, em **Homologação**. Lentamente a quantidade de tarefas por semana aumentou significamente, como também, diminuiu as tarefas que eram iniciadas e ficavam paradas por algum impedimento técnico, organização ou cliente.

Esta mudança também significou que a maioria desenvolvedores de fato se responsabilizavam pelas funcionalidades, ou correções de bugs até o cliente interno/externo e dar o aceite para finalizar de fato a tarefa. Isso também ficou evidente ao olhar o Pipeline, diminuiu a quantidade de código que entra em produção por commit e aumento a quantidade de commits realizados por mês em produção. 

Outro efeito positivo é que a throughput das entregas continua a mesma de antes da implementação do Kanban. O ganho de produtividade das equipes significou a possibilidade de desenvolver as funcionalidades, fazer as correções sem que tenha que trabalhar de forma exaustiva para fazer as entregas.

**Cumulative Flow Diagrama com WIP estabelecido**
![](/images/CumulativeFlowDiagram_WIP.png)

Há muito por fazer mas mostra que processos quando bem aplicados podem transformar uma organização, um pouco desta história foi contada na apresentação abaixo.

<script async class="speakerdeck-embed" data-id="ec9e2e0c2257405080121b334fe62e6a" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>
