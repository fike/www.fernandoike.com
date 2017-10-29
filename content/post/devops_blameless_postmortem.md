+++
title = "Blameless Postmortem"
date = 2017-09-07T16:02:54-03:00
draft = false
description = "Segunda parte sobre Blameless (Postmortem)"
categories = ["devops", "portugues", "blameless"]
tags = ["devops", "portugues", "blameless", "postmortem", "toyota", "gitlab", "etsy", "morgue"]
+++
![](/images/office_report.jpg)

Esta é a segunda parte sobre Blameless, a primeira parte está [aqui](https://www.fernandoike.com/2017/08/21/blameless-a-culpa-não-é-sua/). Recomendo que leia ela antes de ler este texto.

Postmortem também é conhecido por outros nomes (Retrospectiva de projeto, Revisão de melhoria de qualidade, Laudo pós-incidente, Análise revisão de projeto, etc.). No universo de TI está se tornando comum usar o termo Blameless Postmortem para o relatório depois de um incidente identificando as causas da interrupção/falha de um serviço sem apontar como culpado as pessoas, mas sim identificar no processo as falhas e corrigí-las.

O relatório Blameless Postmortem mais conhecido é da Gitlab sobre um incidente no início de 2017. Ele é uma excelente referência de como fazer um: mostra o que eles fizeram para corrigir, a identificação porque ocorreu o incidente e as melhorias que poderiam implantar para que não ocorra novamente. Importante destacar para **"não fazer (postmortem) exatamente como eles fizeram, a cultura deles é muito diferente e muito difícil de ser reproduzida"**. Muitas organizações fazem de forma similar mas não tornam público todas as informações sobre um incidente. Compartilham o máximo possível para que todos (dentro da organização) aprendam também.

Blameless Postmortem não é só relatórios de pós-incidente, os relatórios são o resultado da cultura Blameless e DevOps. Não culpar humanos deve ser um mantra dentro de uma organização, [Dave Zwieback](https://twitter.com/mindweather) em "The human side of Postmortems" ressalta: "*Sua organização deve continuamente afirmar que os indivíduos nunca irão ser a 'causa raiz' das interrupções*", isso deve ser reforçado pelos líderes de equipe e da organização senão o Postmortem tenderá a culpar o erro humano.

### O sistema caiu e agora?

Supondo que um sistema caiu, como proceder com o Postmortem do incidente.  Algumas organizações preferem destacar alguém da equipe para escrever o documento enquantos as outras pessoas da equipe e outras equipes tratam de resolver o incidente. Outras organizações preferem criar um documento único (Google Docs ou uma [Wiki](https://en.wikipedia.org/wiki/Wiki)) em que todos da organização possam ver o que está sendo escrito e também contribuir com informações sobre o incidente. Eu, particularmente, prefiro adotar alguma coisa visual como whiteboard e criar uma timeline como a imagem de um incidente no HootSuite. É onde os times que estão atuando para resolver o problema podem tentar montar um histórico dos fatos que geraram o incidente, impactos e ações que estão sendo tomadas para resolver.

Organizações em que as equipes trabalham remotamente é mais difícil trabalhar com Whitboard, o uso do chat(Ops) ([IRC](https://en.wikipedia.org/wiki/Internet_Relay_Chat), Slack, etc) é melhor lugar para concentrar as informações mais importantes, anunciar para todos da organização as ações que estão sendo tomadas e convocar quem for necessário para atuar. Importante que haja um documento  complementar onde possa detalhar o máximo possível e que seja de acesso a todos na organização. A [Etsy](https://) criou um sistema chamado [Morgue](https://github.com/etsy/morgue) com essa finalidade.

Numa empresa que trabalhei o tratamento dos incidentes graves eram gerenciado da seguinte maneira:

#### Sala de Guerra (War room) por chat e conf call
  A maioria das equipes trabalhavam em escritórios distantes ou em casa. O principal meio de comunicação da empresa era o Slack e nos incidentes graves o usávamos discutir um incidente. Todo mundo da empresa podia interagir nos canais de Operação para obter informações sobre incidente e avisar os clientes. Também era aberto um conferência de áudio com as pessoas mais relevantes para tratar o incidente.

#### Documentando o incidente na Wiki
  Os detalhes sobre o incidente, timeline com os acontecimentos e as lições aprendidas eram escritos numa página na Wiki da empresa em que todos tinham acesso. Essa página do incidente posteriormente seria base da comunicação à todos os clientes da empresa.

#### Comunicação aos clientes
  Os clientes que estavam foram impactados eram comunicados imediatamente (email ou telefone) e todos os outros em seguida via email de forma resumida a(s) causa(s) do incidente, a solução de contorno e as ações de longo prazo para que aquele incidente não ocorresse novamente.

Esta empresa que trabalhei usava inconscientemente os **3 R** proposto por Dave Zwieback em **The human side of Postmortem**.

#### Regret - Arrependimento
- Um reconhecimento do impacto da interrupção e um pedido de desculpa.

#### Reason - Razão
- Uma linha do tempo da interrupção, do incidente inicialmente detectado até a resolução, incluindo o assim chamado "causa raiz"

#### Remedy - Solução (contorno)
-  Uma lista dos itens solucionados para garantir que esta interrupção não irá se repetir


Uma abordagem parecida é a usada na Etsy e relatada (a primeira vez) por John Allspaw na Etsy em [Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/), No texto dele é destacada mais o lado humano de um Postmortem.

- Quais ações eles tomaram e em que momento
- Quais os efeitos que eles observaram
- As expectativas que eles tinham
- As suposições que eles fizeram
- A compreensão deles da linha do tempo dos eventos que ocorrerão

- ... E que eles possam dar o relato detalhado sem medo de punição ou retaliação

**Victor Ops** tem um excelente checklist para Postmortem que também pode usado:

- Documentar sua linha do tempo ou os dados de log
- Documente as conversas
- Deixe espaços para notas
- Média de tempo para resolução / Outros cálculos de tempo
- Nível de severidade
- Arquive-os para recuperação histórica
- Remediação - torne-o acionável

E por fim e complementar o **5 Whys** (Por quês).

5 Whys é uma técnica interrogativa iterativa criada por [Sakichi Toy](https://www.toyota-industries.com/company//history/toyoda_sakichi/)oda para explorar a relação de causa-efeito  de um determinado problema no processo fabril na [Toyota](https://www.toyota.com). O [Asian Development Bank](https://www.adb.org/) descreve como três elementos chaves para usar 5 Whys de forma efetiva.

- Descrições exatas e completa dos problemas
- Honestidade completa em responder as perguntas
- A determinação de ir a fundo nos problemas e resolvê-los

Como mencionado no início do texto, a [Gitlab](https://gitlab.com/) tem um do [Postmortem](https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31) mais completo que já li e recomendo muito a leitura dele com o cuidado de não focar somente na parte técnica da resolução do incidente mas o contexto das técnicas e frameworks que usaram. Se quiser ler uma das aplicações do 5 whys neste Postmortem em português, leia meu texto "[O Postmortem da Gilab](https://www.fernandoike.com/2017/02/13/o-postmortem-da-gitlab/)"

Postmortems são um excelente oportunidade de aprender a partir da experiência dos outros, também mostram que as organizações superstar também tem incidentes e aprendem com eles constantemente. [Dan Luu](https://) criou um [repositório git](https://github.com/danluu/post-mortems) com diversos Postmortem que vale uma leitura e conversa sobre alguns deles com as equipes de trabalha.

**Referências** :

Practical Postmortems at Etsy: https://www.infoq.com/articles/postmortems-etsy

How to Conduct a Blameless Security Post-Mortem: https://www.pagerduty.com/blog/blameless-post-mortems-strategies-for-success/

5 Whys – how we conduct blameless post-mortems after something goes wrong: http://code.hootsuite.com/blameless-post-mortems/

Blameless postmortems – strategies for success: https://www.pagerduty.com/blog/blameless-post-mortems-strategies-for-success/

Dan Luu - Postmortem repository: https://github.com/danluu/post-mortems

The Five Whys Technique: https://www.adb.org/sites/default/files/publication/27641/five-whys-technique.pdf

Debriefing Facilitation Guide: https://extfiles.etsy.com/DebriefingFacilitationGuide.pdf

Helping Better Understand Events by Building a Post Mortem Tool: https://vimeo.com/77206751
