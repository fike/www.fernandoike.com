+++
categories = []
date = "2017-06-17T21:56:11-03:00"
description = ""
draft = true
tags = []
title = "Infraestrutura Ágil tem que morrer"

+++
O termo Infraestrutura Ágil em português nasceu como um recorte do DevOps, a ideia da concepção era que fosse uma preparação para implantar DevOps. Naquela época havia uma resistência ao DevOps, principalmente em Operações. A crença na época era que isso facilitaria o processo de implantação da Cultura DevOps nas organizações. Um dos objetivos era desviar do processo do termo DevOps torna-se um buzzword, infelizmente este desvio mostrou equivocado e tornou-se um buzzword também. O pior de um buzzword não é um conceito certo seja desvirtuado, é um conceito equivocado torna-se um buzzword porque não é possível corrigir afirmando que o conceito original estava certo.

Como sou um dos [signatários](https://web.archive.org/web/20160818034746/http://infraagil.io:80/alliance/) deste equivoco conceito, cabe uma reflexão e autocrítica. No [texto](https://www.fernandoike.com/2017/03/23/site-reliability-engineer---sre/) que escrevi sobre [SRE](https://www.fernandoike.com/2017/03/23/site-reliability-engineer---sre/) já fazia essa autocrítica mas talvez não de forma clara. Infraestrutura Ágil como conceito nunca deveria ter existido, portanto, deve morrer.

## Porque Infraestrutura Ágil é um equívoco conceitual

Patrick Debois e Andrew Shafer tiveram a famosa conversa sobre [Agile Infrastructure](http://www.jedi.be/presentations/agile-infrastructure-agile2008.pdf), o tema ali era como Infraestrutura/Operações poderia aplicar as práticas Agile que as equipes de desenvolvimento faziam até então. Logo em seguida (no ano seguinte) John Allspaw e Paul Hammond [contaram](https://www.slideshare.net/jallspaw/10-deploys-per-day-dev-and-ops-cooperation-at-flickr/) como no Flickr a colaboração entre Devs e Ops aumentou a produtividade, estabilidade e confiabilidade dos serviços

Em seguida no mesmo ano, Patrick Debois realiza o primeiro DevOpsDays em Ghent e partir daí começou um processo de pensamento sistêmico (system thinking) tornando as organizações altamente produtivas. O que fizemos ao propor Infraestrutura Ágil foi regredir para antes de 2008 ou pior, porque as referências do Agile foram deixadas de lado.

Este recorte da Cultura DevOps gerou um efeito colateral da aplicação da Automação (Automation) e Medições/Métricas/Monitoramento (Measurement), Cultura (Culture) e Compartilhamento (Sharing) ficaram relegados ao segundo plano. [No texto de John Willis](https://blog.chef.io/2010/07/16/what-devops-means-to-me/) sobre **CAMS** ele já definia assim.

**C**ulture = "*Pessoas e processo primeiro. Se você não tem a cultura, todo o esforço da automação será infrutífero*"

**A**utomation = "*Este é um dos lugares para você começar entender sua cultura. Neste ponto, as ferramentas permitem iniciar a fábrica da automação para DevOps*"

**M**easurement = "*Se você não consegue medir, você não consegue evoluir. Uma implementação DevOps bem sucedida medirá tudo o quão frequente possível… métricas de performance, processo e mesmo métrica de pessoas*"

**S**haring = "*Compartilhamento é loopback no ciclo do CAMS. É fundamental criar a cultura onde as pessoas compartilham idéias e problemas.*"

### Infraestrutura Ágil é um Anti-Pattern da Cultura DevOps

Ao aplicar Infraestrutura Ágil, supõe-se que há um ganho incrível no gerenciamento da infraestrutura de uma organização, isso é evidenciado quando se aplica gerencia de configuração usando Infraestrutura como código e/ou aplicando o Continuous Delivery. Estas organizações estão aplicando parcialmente o CAMS, de fato não vêem melhora em algumas indicadores da cadeia de produção que estão além do tempo de repostas do ping ou uptime. Você sabe se o MTTR diminui, há alguma métrica de aplicação como tempo resposta da aplicação? A frequência dos deploys aumentou? O lead time entre versões diminuiu? Há um algum indicador que mostre que a qualidade do software melhorou?

O State of DevOps Report de 2017 mostra que a diferença de vários indicadores entre organizações de alta performance e baixa diminuiu. O relatório indica que esta diminuição é porque as organizações com baixa performance melhoram o rendimento, porém identificou que o MTTR (tempo de recuperação) aumentou. A minha opinião é que nestes locais há um descompasso entre Devs e Ops, não há um ganho de produtividade da organização, apenas de uma das equipes. A aplicação da Infraestrutura Ágil aumenta este descompasso.

A Infraestrutura Ágil também respondia ao problema de comunicação, confiança dentro do silo (equipe) de Infraestutura. John Allspaw no texto sobre Blameless defini os 7 passos da vergonha (culpa), ele se refere a relação entre gerência e equipe mas é aplicável entre os membros de uma equipe também.

1. Engenheiro tomam atitude e contribuem para uma falha ou acidente.
2. Engenheiro é punido, envergonhado, culpado ou reprimido.
3. Reduz a confiança entre engenheiros e a gerência fica procurando alguém como bode expiatório.
4. Engenheiros ficam em silêncio sobre detalhes de ações/situações/observações, resultando na engenharia de "Cover-Your-Ass (pelo medo de punição)
5. Gerentes tornam-se menos conscientes e informados sobre o desempenho do trabalho do dia a dia, engenheiros se tornam menos educados na espreita ou condição latente para falha devido ao silêncio mencionado no passo **#4**.
6. Erros tornam-se mais prováveis, condição latente para eles não serem identificadas devido ao passo **#5**
7. Repete a partir do passo **#1**

A aplicação de Infraestutura Ágil em Operações era resolver o problema de comunicação, confiança e tornando-a mais produtiva. O efeito colateral desta assimetria de produtividade é conseguir atingir as metas da organização pois a melhora de produtividade não atinge o processo produtivo dela, somente a otimização de uma parte da organização. O Lean, um dos princípios que a Cultura DevOps é fortemente inspirada, define-se: "*Uma cultura que cria mais valor para os usuários com menos recursos, mudando o foco da otimização isolada para otimização de fluxos de produtos e serviços através de todo o cadeia de valor (value stream) horizontalizado em toda a organização*".

Portanto, ao implementar a Infraestutura Ágil, está aplicando um Anti-Pattern da Cultura DevOps.

### Então, como faz?

Quando fizemos o recorte de DevOps focado em Operações como Infraestrutura Ágil, nós simplificamos a Cultura DevOps fortemente no CAMS e esquecemos que ele é o resultado, segundo The DevOps Handbook, "*...da aplicação dos princípios mais confiáveis da manufatura física e liderança para a cadeia de valor de TI. DevOps depende do conhecimento do Lean, Teoria das Restrições (Theory of Constraints), Toyota Production System, engenharia de resiliência, organizações dispostas a aprender, cultura de segurança, fatores humanos e muitos outros. Outros contextos valiosos DevOps se inspira incluem cultura de gerenciamento de alta confiança, servant leadership e gerenciamento de mudanças organizacionais.*".

A implementação da cultura DevOps passa pelo The Three Way (Os Três Caminhos) de Gene Kim. Ele descreve no IT Revolution The Three Way como "... os valores e filosofias que enquadram os processo, procedimentos e práticas DevOps, bem como as etapas recomendas".

1. The First Way - O princípio do fluxos, qual acelera a entrega do trabalho do Desenvolvimento para Operações, e então para nosso clientes

2. The Second Way - O princípio do Feedback, qual nos permite criar sempre um sistema mais seguro de trabalho

3. The Third Way - O princípio do Aprendizado Contínuo e Experimentação promovem uma cultura de alta-confiança e uma abordagem científica para tomada de risco da melhoria organizacional e parte do nosso trabalho diário
