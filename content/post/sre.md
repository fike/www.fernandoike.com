+++
draft = false
date = "2017-03-23T21:01:08-03:00"
title = "Site Reliability Engineer - SRE"
description = "O que é SRE"
categories = ["devops", "sre", "portugues"]
tags = ["portugues", "devops", "sre", "blameless", "postmortem", "agile"]

+++
Se ainda não viu uma vaga de trabalho ou mesmo só a sigla SRE, então se prepare porque a tendência é tornar-se bem popular. O acrônimo SRE é usado para descrever tanto **Site Reliability Engineering** ("Disciplina/Cultura") **como Site Reliability Engineer** (descrição de função/vaga de trabalho). O termo foi criado em 2003 por [Ben Treynor](https://www.linkedin.com/in/benjamin-treynor-sloss-207120/), atual VP de Engenharia do Google e ele relata sobre a criação da equipe no livro [Site Reliability Engineering](https://landing.google.com/sre/book/). (tradução livre)

> SRE é o que acontece quando você pergunta para um engenheiro de software para projetar uma equipe de operações. Quando entrei no Google em 2003 e recebi a tarefa de gerenciar uma "Equipe de Produção" de sete engenheiros, durante a minha vida fui engenheiro de software até aquele ponto. Então, projetei e gerenciei o grupo da maneira que eu gostaria que ele funcionasse, se eu trabalhasse como um SRE. Desde então, esse grupo amadureceu para se tornar a equipe atual de SRE do Google que permanece fiel a suas origens como previsto por engenheiro de software ao longo da vida

Treynor define um pouco melhor ao final do capítulo introdutório do mesmo livro. (tradução livre)

>*Site Reliability Engineer representa uma ruptura significativa das melhores práticas da indústria existente para gerenciar serviços grande e complicados. Motivado originalmente pela familiaridade - "como um engenheiro de software, isso é como gostaria de investir meu tempo para realizar um conjunto de tarefas repetitivas" - tornou-se muito mais: um conjunto de princípios, práticas, incentivos e um campo de atuação dentro de disciplina maior que é a engenharia de software*.

Recomendo ler o livro do Google sobre SRE, ele mostra boas práticas para área de operações de TI de uma organização. Neste texto vou destacar alguns pontos que achei mais interessantes e também expressar minhas impressões e experiências similares. Logo no início, Treynor descreve como funciona a TI no modelo tradicional, equipes de desenvolvimento e operações trabalhando como silos, áreas de baixa interação e muitos conflitos entre elas. Ele define a função de sysadmin de TI ligado a processos tradicionais de TI, não concordo com esse conceito. Afinal, em quase uma década após DevOps ser cunhado (2008), os sysadmins tiveram uma mudança significativa como função e também em importância ao lidar com automação da infraestrutura e serviços na nuvem (cloud).   

Quando Guto Carvalho e outros conversamos sobre a definição de [Infraestrutura Ágil](http://infraagil.io/), ali tentava-se delimitar um conjunto de princípio, práticas e disciplinas para área de operações de uma organização. De fato isso foi definido e pode ser lido [aqui](http://infraagil.io/), contudo ao aprofundar um pouco meu estudo sobre DevOps e SRE, considero que SRE faz mais sentido para ser aplicado nas organizações (empresas, repartições públicas, etc.). Afinal, são mais de uma década de experiência em manter sistemas gigantes, escaláveis e resilientes (Google).

## DevOps ou SRE

A similaridade entre SRE e Infra(estrutura) Ágil fica evidente quando Treynor tenta definir SRE do pontos de vista de "DevOps". (tradução livre)

>*O termo "DevOps" emergiu na indústria no fim de 2008 e como este texto foi escrito (início de 2016) está num estado de fluxo. Seus princípios principais - envolvimento das funções de TI em cada fase da definição e desenvolvimento de um sistema, forte dependência da automação versus esforço humano, a aplicação das práticas de engenharia e ferramentas para tarefas operacionais - são consistentes com muitas práticas e princípios de SRE. Poderia ver o DevOps como uma generalização de vários princípios fundamentais para uma ampla e vasta gama de organizações, estruturas de gestão e pessoal. Poderia, de forma equivalente, ver o SRE como uma implementação do DevOps com algumas extensões peculiares.*

O que é SRE faz?

Basicamente um time SRE é responsável pela **disponibilidade**, **latência**, **desempenho**, **eficiência**, **gerenciamento de mudança**, **monitoramento**, **resposta a emergência** e **plano de capacidade** (capacity planning) dos serviços que eles são responsáveis (ex: SRE não é responsável pela manutenção de impressoras, etc.). Também não quer dizer que eles são responsáveis somente pela Operação de TI, há uma grande interação com outros times e sempre mantendo o foco no trabalho de engenharia e não somente no trabalho operacional.

Ao ver os princípios que definem a disciplina SRE, poderá observar que há uma intrínseca abordagem ao **C.A.M.S.** (**Culture**, **Automation**, **Measurement**, **Sharing**), como também ao **The Tree Ways** (**Systems Thinking**, **Amplify Feedbacks**, **Culture Of Continual Experimentation and Learning**). Claro que a comparação direta entre SRE e DevOps não mostrará a relação de forma tão evidente, mas de fato estão lá. DevOps é  definido de maneiras diferentes e geralmente usa-se definições abertas, por exemplo: Minha definição é "*DevOps significa uma cultura que permitir as organizações alterar seus processos, transformando-se de organizações de baixa performance em alta.*". O Gartner [define](http://www.gartner.com/it-glossary/devops/) como - "*DevOps representa uma mudança na cultura da TI, focando na entrega rápida dos serviços de TI através da adoção do Agile, práticas Lean no contexto de um abordagem orientada à sistema. DevOps enfatiza pessoas (e cultura), procura melhorar a colaboração entre equipes de desenvolvimento e operações. As implementações DevOps utilizam tecnologia - especialmente ferramentas de automação que podem alavancar uma infraestrutura cada vez mais dinâmica e programável a partir de uma perspectiva de um ciclo de vida.*" . Já SRE é um pouco mais direto, seja como disciplina ou como uma função de trabalho numa organização a definição é mais clara, como já citado no início deste texto.

## As Equipes

As equipes SRE são compostas por uma mescla que de pessoas com mais conhecimento em desenvolvimento de software e outras com maior conhecimento em administração de sistemas. As equipes são compostas por pessoas de diferentes conhecimentos, permitindo uma troca intensa de conhecimento entre os membros, um intenso e rápido aprendizado. Interessante que não há a função do Arquiteto (Software, Sistemas, Rede, etc), no artigo "[Hiring Site Reliability Engineers](https://www.usenix.org/publications/login/june15/hiring-site-reliability-engineers)" publicado [The Usenix Magazine](https://www.usenix.org/publications/login) é explicado porque não tem "**arquitetos**" - "**Nós especificamente não olhamos para *"arquitetos"* - porque é uma função que simplesmente não existe no Google: todos da nossa engenharia projetam como também desenvolvem.**"

O tempo das equipes é divido entre atividades de rotina da Operação de TI como: tickets, problemas de indisponibilidade, suporte, plantão, etc. Como também atividades relacionadas as habilidades deles de código para projetos como automação, projetos de infraestrutura, etc. Não somente automação usando uma ferramenta de configuração como Puppet ou Chef, mas desenvolvendo ferramentas de automação. O tempo do trabalho é divido entre 50% para atividades tradicionais de suporte e os outros 50% aos projetos do trabalho que podem ser de simples automação como desenvolver serviços para serem usados na própria equipe ou interações com as equipes. Uma fração deste tempo (5%) também é direcionada para interações com as equipes de desenvolvimento de produtos, este tempo com os desenvolvedores ajudam a evitar indisponibilidade de um futuro serviço, possibilitando o compartilhamento boas práticas de aplicadas em outros projetos.

Há também a liberdade do profissional SRE de mudar de equipe por alguma razão. Geralmente, a saída de um membro de uma equipe na Operação impacta na atividade dos outros da equipe. No Google, este impacto é relativamente pequeno porque todas equipes usam os mesmos processos e princípios. Por exemplo, se uma pessoa decidir mudar de equipe porque quer um novo desafio mas ele não tem conhecimento do framework usado pela outra equipe, isso não é um impeditivo para mudança já que os processo são os mesmo, ele aprenderá a rotina e o framework rapidamente. Outro ponto interessante é que no processo de recrutamento de novos SRE, não é requisito saber as linguagens e frameworks usados pelo Google, o mais relevante é que o candidato saber programar (**Coders**).

A educação contínua é também parte importante da cultura SRE, os SRE são encorajados de diversas maneiras a aprender continuamente, como também ensinar os SREs menos experientes. Isso ocorre de diversas formas, desde simulações de incidentes de indisponibilidade famosos já ocorridos, como acompanhamento de atendimento como sombra (shadow on-call). Também são incentivados a fazer engenharia reversa, mas não da forma que você está imaginando: descompilando um binário, etc. Um bom exemplo e comum em muitas empresas é suportar um sistema com a documentação incompleta ou desatualizada, sysadmins (e outros de Operações de TI) vão tateando sistemas até entender como eles funcionam e os principais que ele tem.

As equipes SREs não são equipes isoladas, elas se relacionam com diversas outras equipes. Além as equipes de produtos, eles também têm forte interação com os
*Release Engineers* e *Launch Coordination Engineering*. Os equipes LCE são equipes de consultoria interna de profissionais SRE com experiência em lançamento de produtos/serviços, orientando "**... os desenvolvedores para a construção de produtos rápidos e confiáveis que atendam aos padrões do Google em confiabilidade, escalabilidade e robustez**" - *(Cap. 27 - Reliable Product Launches at Scale - SRE Book)*. As equipes RE - "... **definem as melhores práticas para usar nossas ferramentas para garantir que os projetos serão lançados usando metodologias consistentes e repetíveis. Nossas melhoras práticas cobrem todos elementos de um processo de lançamento.**" - *(Cap. 8 - Release Engineering)*

##  Os princípios básicos de SRE

Os princípios básicos de SRE são:

- Garantia um foco duradouro na Engenharia
- Perseguindo a maior velocidade de mudança sem violar um serviço SLO
- Monitoramento
- Resposta a emergências
- Gerenciamento de mudança
- Previsão de demanda e Capacity Planning
- Provisionamento
- Eficiência e Performance

Abaixo comento alguns deles.

### Garantia um foco duradouro na Engenharia

Como mencionado no início do texto, os SRE trabalham 50% em atividades típicas de área de operações de TI de uma organização. Quando este percentual se eleva, as atividades excedentes são direcionadas para os times de desenvolvimento de produto ou por um tempo determinado é alocado SREs de outras equipes para ajudar.

### Perseguindo a maior velocidade de mudança sem violar um serviço SLO

Saber o que é **S**ervice **L**evel **O**bjective? No ITIL V3 ele mudou para **S**ervice **L**evel **T**arget, importante não confundir com **S**ervice **L**evel **A**greement. Exemplos bem simplistas de SLO e SLA: Servidores Web devem ter disponibilidade acima de 96% (SLO) medido pelo monitoramento pela monitoramento da Foobar Galaxy Company (a mesma empresa responsável pelos servidores web), a Overdrive IaaS tem SLA de 99% de disponibilidade da sua infraestrutura em contrato com a Foobar. Sacou? SLO é uma medida internamente pela Foobar e SLA é sempre um "acordo" entre partes, na nuvem (cloud) é acordo de disponibilidade ou performance oferecido pelos fornecedores como IaaS, SaaS, PaaS, etc.

Como definir o SLO de um serviço ou aplicação?

Talvez seja um dos pontos de maior conflito entre áreas de TI e/ou mesmo outras áreas de uma organização. A área de operações pode definir que o SLO é de 97% de disponibilidade, mas desenvolvimento ou a gerencia querer 100%. Inúmeras vezes já tive que explicar o quanto é inatingível e custoso é 100% de disponibilidade. Umas das respostas mais comum era - "Ah, então o mais próximo de 100%. 99,99%, ok?". - A frustração ao ouvir este tipo de resposta era grande porque sentia que eu era responsável por não conseguir explicar a dificuldade de alcançar 100%. Para conseguir convencê-los, mostrava financeiramente o tão custoso era atingir a meta e se eles estavam dispostos a arcar financeiramente. A maioria absoluta desistia e era definido um valor mais factível. Ainda me sentia frustrado porque era muito tempo desperdiçado para definir a disponibilidade do serviço.

O Google via SRE tem uma abordagem melhor, eles a chamam de **Error Budget**. Ele é definido pelo inverso do SLO, exemplo: o SLO é de 99%, então o Error Budget é de 1%, portanto, 1% de indisponibilidade é o permitido para incidentes de indisponibilidade. Claro que este valor não era fixo eternamente, ele pode variar, por exemplo, no lançamento de um serviço o Error Budget pode ser maior e posteriormente ajustar para um valor menor.  

### Monitoramento

Provavelmente, você trabalhar com monitoramento de maneira similar aos SRE no Google. Eles usam diversos métodos para monitorar seus serviços, poderia ser um outro texto só sobre o assunto, mas está pensando numa implantação inicial ou revisão do monitoramento do seu ambiente, vale usar o que eles chamam de "Os quatros sinais de ouro" (**The Four Golden Signals**): **latência**, **tráfego**, **erros** e **saturação** para coleta de dados. O monitoramento gera três tipos de saída: alertas, tickets e logs. É enfatizado no livro que as saídas devem ter informações úteis e simplificar o possível sem que seja simplista. Por exemplo: configurar além de somente "pings" para avaliar a disponibilidade de um serviço. Ah, recomendam fazer usar como sistema de monitoramento com armazenamento do tipo time-series como [Prometheus](https://prometheus.io)

Não precisa mudar seu sistema de monitoramento de um dia para outro, você melhorar as métricas sem fazer a migração. O importante é configurar as informações que são realmente importantes para vocês e a empresa. Por exemplo: Numa empresa que trabalhei alguns anos atrás, tínhamos um sistema de monitoramento que "não monitorava" segundo alguns dos meus colegas. Ninguém confiava nele para receber alertas de saturação de discos, rede ou memória, etc. Eles preferiam entrar nos servidores manualmente olharem por si, portanto, a confiança do monitoramento era zero. Alguns diziam que o problema era ferramenta, então deveria trocar por outra. Outros diziam que não tinha ninguém ali entendia do assunto e por isso que não funcionava.

Contratamos uma pessoa "resolver" com experiência em monitoramento, ele reimplementou o monitoramento e ninguém falava mais disso, tudo certo? Passado algumas semanas, perguntei por que o monitoramento estava com tantos alertas em vermelho. A resposta foi que os estavam usando o template padrão do sistema de monitoramento e também não gerava ticket automatizados na fila deles. Bom, decidimos mudar a abordagem, inicialmente monitorávamos somente o básico de cada servidor (CPU, memória e disco), caso um algum indicador tivesse valor maior que o threshold, era aberto um ticket para Operações. Posteriormente foi incorporando outras métricas, as métricas ainda não eram como os Quatros Sinais de Ouro, mas o dashboard do sistema de monitoramento só tinha alertas (vermelho) quando realmente tinha algum problema.

Uma das pessoas da equipe disse uma vez (infelizmente não quem foi) - "*As informações do monitoramento só são úteis se as pessoas ou robôs souberem o que fazer com elas.*

### Resposta a emergências

Na maioria absoluta dos lugares que trabalhei na área de Operações de TI, o indicador mais importante era sempre o **MTTF** (Mean Time to Failure), mas e não só eles (Google) consideram tão importante ou mais o **MTTR** (Mean Time to Repair).

Faz sentido, não? Uma vez o presidente da empresa que eu trabalhava perguntou se o novo site da empresa iria cair, afirmei que provavelmente sim. Ele me olhou indignado (furioso) sem dizer uma palavra, em seguida respondi: "*Sistemas são como carros, sempre tem alguma manutenção para fazer e nem sempre você consegue prever o que irá quebrar no carro.*". Bom, passado alguns meses estávamos conversando (Diretor de TI e eu) sobre uma RFP para contratação de um serviço especializado para a área de Operações e queria entender sobre MTBF (Mean Time Between Failures), MTTF e MTTR. Expliquei para ele o significado deles e ele perguntou porque tinha colocado o MTTR tão baixo para um serviço especializado que estava contratando. A resposta foi - "*Se um sistema não falhar durante um ano, ninguém vai lembrar da importância dele, mas se ele ficar indisponível por algumas horas nossas vidas serão um inferno até ele voltar.*"

O Google identificou que o MTTR melhorou até 3 vezes ao usarem um playbook (em alguns lugares é conhecido como runbook). Ele é muito usado em outras indústrias e órgãos governamentais que precisam responder por incidente como desastres, ameaças a segurança, etc. O playbook deve ser claro sobre como tratar um mais incidentes de emergência como: procedimentos a serem executados, fluxo do processo e escalonamento de pessoas. Na empresa de telecom que trabalhei há muitos (muitos) anos atrás existia um playbook para incidentes emergenciais que poucas pessoas usavam, num plantão de um membro da equipe teve um incidente de sistema importante (billing), ele ficou apavorado e me ligou para saber o que fazer. Perguntei se ele tinha olhado o playbook porque lá tinha o contato da equipe de produto responsável e os primeiros procedimentos para fazer. Ele não tinha visto, nem ele e nem o restante da equipe tinha lido. A principal razão alegada (com razão) é que o documento era longo e difícil entender, soma-se a dificuldade de saber qual era a versão mais atual dele porque cada membro da equipe tinha uma versão diferente. Apesar de ter uma Wiki, ninguém a usava para este tipo de informação.

Um dos exercícios mais interessantes usado pelo Google é a "**Wheel of Misfortune**" (A roda do azar?). São simulações de incidentes que já ocorreram no passado em que semanalmente um membro da equipe de SRE é escolhido para fazer a simulação. Este tipo de exercício é excelente para acelerar o aprendizado e também preparar o SRE para situações do plantão, além de possibilitar formas de resolver os incidentes.

### Gerenciamento de Mudança

Este é um número interessante, 70% dos problemas de indisponibilidade estão relacionados às mudanças em sistemas em produção. Eles recomendam:

- Implementar lançamentos (rollouts) progressivos
- Detecção rápida e precisa dos problemas
- Rollback com segurança quando os problemas surgirem

Além dos princípios básicos, outros assuntos que se destacam (para mim) são Posmortem, Testes, PRR model (Production Readiness Review)

## (Blameless) Postmortem

O Google não cita Postmortem como um dos princípios básicos de SRE mas na minha visão a cultura de Postmortem é chave para eles e qualquer organização que deseja se torna organizações de alta performance. Os documentos Postmortem são importantes como memória de um incidente, entendendo porque um incidente aconteceu, o que foi realizado para resolver e ações posteriores para que não ocorra novamente. Eles podem ser feitos de diversas formas, tem lugares que usam páginas wiki, outros criam um documento no Google Docs que é atualizado simultaneamente pelas pessoas envolvidas no incidente. Também já vi criarem um timeline com post-it, etc. O fundamental que os relatórios Postmortem não devem apontar para pessoa(s) especificamente, eles devem focar nos acontecimentos e processos.

Para eles os pontos em comum nos documentos postmortem devem incluir:

- Período de downtime visível pelos usuários ou degradação além de um certo threshold
- Qualquer tipo de dados perdido
- Intervenção dos engenheiros (rollback de versão, alteração do roteamento do tráfego, etc)
- Um tempo de resolução acima de algum threshold
- Uma falha do monitoramento (qual geralmente implica na descoberta manual de um incidente)

Obviamente é usado o Google Docs para os documentos postmortem mas eles definem três pontos chaves para qualquer ferramenta de postmortem:

- Colaboração em tempo real
- Um sistema aberto para comentários/anotação
- Notificações por email

Também devem responder as seguintes perguntas:

- Os principais dados do incidente foram coletados para serem analisados posteriormente?
- As avaliações do impacto estão completas?
- A causa raiz foi suficientemente identificada?
- O plano de ação é apropriado e o resultado do conserto do bug está na prioridade apropriada?
- Nós compartilhamos os resultados com os stakeholders relevantes?

E para qual público esses documentos são destinados? Separei uma frase do capítulo "[Postmortem Culture: Learning from Failure](https://landing.google.com/sre/book/chapters/postmortem-culture.html)" que define bem:

> "Nosso objetivo é compartilhar postmortems para a maior audiência possível que poderá ser beneficiada do conhecimento ou lições aprendidas."

## Testando a Confiabilidade

Em **Respostas a Emergências** mencionei a maior relevância do MTTR do que MTBF, no [capítulo (17)](https://landing.google.com/sre/book/chapters/testing-reliability.html) sobre **Testes** eles mostram como testes pode ajudar a encontrar bugs antes de irem para o ambiente de produção. Assim, melhorando o MTBF significativamente.

Os tipos de testes são variados, desde os mais conhecidos como: Testes Unitários e Testes de Integração à outros como Testes de Regressão e Testes de Configuração. Ah, sim! Meus tipos de testes favoritos: Testes de Stress e Testes de Desastres.

Outros testes que não mencionado mas considero relevante são os testes de segurança como Pen Tests, Auditorias, Análise Estática de Código, etc.

## Conclusão

SRE usa muito da cultura ágil como também tem muito da cultura DevOps, a grande diferença (para mim) é que as disciplina envolvidas em SRE são visíveis e o entendimento sobre o que SRE é conciso, diferentemente de DevOps que cada um tem uma interpretação diferente do que é. Não mencionado explicitamente acima mas vale mencionar é que automação é fortemente utilizada e a estratégia de deploy dos sistemas é o [Canary](https://martinfowler.com/bliki/CanaryRelease.html).

Já vi algumas descrições de vagas SRE em sites de emprego aqui no Brasil, diferentemente de DevOps, SRE pode ser descrito como uma função de trabalho. Talvez não se torne tão popular por alguma restrição do CREA porque a profissão de engenheiro é regulamentada por eles. Então, mesmo que não você não seja um SRE onde trabalha, importante é entender as disciplinas envolvidas e cultura. Provavelmente parte do destacado neste texto ou no livro de SRE do Google você já deve fazer.

No momento, vejo SRE para infraestrutura como uma profunda e metódica forma de transforma a área de operações (infraestrutura) em ambientes altamente resilientes, autônomos (é diferente de automatizado) e de alta confiabilidade. A Tickemaster é um caso interessante e factível para a maioria das organizações, eles têm as funções de SRE como parte da cultura DevOps. Você pode usar SRE e/ou DevOps, ressaltando que o objetivo é transformar a organização de baixa para alta performance.

Referências:

1. SRE Book - https://landing.google.com/sre/book/index.html
2. Are site reliability engineers the next data scientists? -  https://techcrunch.com/2016/03/02/are-site-reliability-engineers-the-next-data-scientists/
3. Error Budge and Risks (Marc Alvidrez) - https://www.usenix.org/conference/srecon15/program/presentation/alvidrez
4. Hiring Site Reliability Engineers - https://www.usenix.org/system/files/login/articles/login_june_07_jones.pdf
5. Canary - https://martinfowler.com/bliki/CanaryRelease.html
