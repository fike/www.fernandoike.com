+++
title = "Continuous Integration Vs Continuous Delivery Vs Continuous Deployment"
date = 2020-07-16T22:50:21-03:00
draft = false
description = "Um revisão sobre Continuous Delivery, Continuous Integration e Continuous Deployment"
categories = ["continuous delivery", "devops", "agile", "portugues"]
tags = ["continuous delivery", "continuous integration", "portugues", "pipeline"]
+++
> Em revisão

O senso comum sobre o papel de Continuous Deployment (Implantação Contínua) é de ele ser a automação após testes (geralmente, de aceitação) serem validados, o artefato segue para implantação no ambiente de produção numa organização. A forma mais comum é mostrar as etapas de um Pipeline (fluxo de trabalho ou workflow) de desenvolvimento de software com as etapas: Construção, Testes, Integração, Testes de Aceitação e Implantação em produção. A quantidade de etapas e quais etapas envolvidas podem variar a depender do texto de referência consultado ou organização, a essência está representada na figura abaixo.

![](/images/cd_classico.png)

Ao olhar para a figura, o primeiro entendimento que Continuous Deployment seria o ciclo mais completo de automação de um Pipeline, Porque a diferença entre ele Continuous Delivery é apenas a automação da implantação em produção. Para alguém que tem pouco conhecimento sobre ciclo de desenvolvimento de software, ela irá entender que Continuous Deployment é mais completo dos três, porque Continuous Integration é um ciclo parcial que não contempla a implantação em produção. Continuous Delivery contém todas as etapas que Continuous Deployment, exceto pela implantação de artefato sendo manual.

O que a maioria dos textos sobre tema descrevem de forma similar a figura acima, representando o Pipeline ed forma sequencial. Continuous Integration primeiro, na sequência Continuous Delivery e por fim, Continuous Deployment.

![](/images/cd_classico-2.png)

## Por que automatizar o Pipeline de desenvolvimento de software?

A maior razão para automatizar é ter um processo de construção de uma versão de software (artefato) reproduzível e auditável. Hoje em organizações com baixa maturidade em engenharia de software, a construção de um artefato é ainda manual, assim como os testes e implantação em produção ser manual. Claro, a automação também gera o benefício de diminuir o Lead Time porque o feedback é mais rápido se o artefato está bom o suficiente para ir a produção.

O Feedback Loop de cada etapa do processo também potencializa a aprendizagem, as políticas de aceitação: cobertura de teste, complexidade de código, integração com outros sistemas, desenvolvimento seguro, etc. mostram para o desenvolvedor o que ele precisa fazer para as novas funcionalidades sejam aceitas no Pipeline. Feedback Loops acontecem em diferentes métodos e frameworks numa organização, não importando tanto qual deles é utilizado. O que realmente importa é o aprendizado das equipes envolvidas a cada iteração e interação no processo de construção de um artefato de software.

![](/images/pipeline.png)

Um commit gera iterações automatizadas com cada etapa de um Pipeline com potencial de ocorrer alguma não conformidade de alguma das etapas, havendo uma ocorrência, todos podem olhar de forma transparente e reproduzível porque aquela não conformidade ocorrer, observar o que é/foi feito para resolver a não conformidade. Isso torna todo o processo transparente para qualquer poder observar e auditar a ocorrência. As restrições impostas no Pipeline são encarada por alguns como burocracia (que de fato é), porém, deve ser encaradas como restrições de um sistema (Sim, [Teoria das Restriçoes]()) para que o artefato construído esteja de acordo com as políticas da organização em diversas perspectivas: segurança, qualidade de engenharia de software, funcionalidades de produto, etc. Elas podem ser uma forma eficiente de aprendizado rápido, como também, uma garantia para implantar em produção um artefato de qualidade aceitável do ponto de vista da organização e para o cliente dela.

Há outros benefícios que são abordados brilhantemente nos livros Continuous Delivery e também no Accelerate, por hora, não será aprofundado neste texto.

## Continuous Integration?

O [site](https://martinfowler.com/articles/continuousIntegration.html) do Martin Fowler tem uma boa descrição sobre Continuous Integration (tradução livre):

> “... é uma prática de desenvolvimento de software onde os membros de uma equipe integram o trabalho com frequência, usualmente cada pessoa integra diariamente - executando para múltiplas integração por dia. Cada integração é verificada por uma construção automatizada (incluindo testes) para detectar erros de integração o mais rápido possível. Muitas equipes acreditam que esta abordagem reduz de forma significativa problemas de integração e permitir um equipe desenvolver software coeso mais rapidamente.”

Isso é evidenciado num Pipeline automatizado com a construção de um artefato. Por exemplo, no momento que uma pessoa envia as modificações para um SCM (Source Code Management) com as modificações realizadas, um serviço de Continuous Integration/Continuous Delivery irá copiar o conteúdo com as modificações(ex: git clone) realizadas, em seguida executa a sequência de etapas configuradas para gerar o artefato, testa e implementa no ambiente de produção (se assim configurado).

## Continuous Delivery?

A melhor definição sobre Continuous Delivery está no site mantido por [Jez Humble](https://twitter.com/jezhumble) (tradução livre):

> “É a capacidade de aplicar as alterações de todos os tipos - incluindo novos recurso, alterações de configuração, correções de bugs e experimentos - em produção ou nas mãos do usuários com segurança e rapidez, de maneira sustentável.”

Esta definição é uma síntese do livro de mesmo nome, escrito por ele por [Dave Farley](https://twitter.com/davefarley77). Importante, não se atenha somente a frase acima, a leitura do livro é super recomendada.

A figura comparativa abaixo entre Continuous Integration, Continuous Delivery e Continuous Deployment não é condiz com a descrição acima. Exceto se isolar o fluxo do Continuous Delivery.

![](/images/cd_classico-3.png)

A automatização de todas etapas de um Pipeline não devem acontecer no dia 1, nem no dia 2. Ela deve ocorrer de uma forma que seja sustentável, evoluindo a maturidade de cada etapa do processo até automatizar a implantação (deploy) dos artefatos em produção.

## Continuous Deployment

Não é só automatizar a implantação em produção como mostrado lá na primeira figura deste texto. É bem mais, Jez Humble no texto [Continuous Delivery vs Continuous Deployment](https://continuousdelivery.com/2010/08/continuous-delivery-vs-continuous-deployment/) diz:

> “Continuous Deployment é a prática de liberar toda boa construção de artefato para os usuários”

Atualmente e também no passado distante, não é só implementar em produção um artefato para os usuários. Envolve estudar quais das diferenças estratégias existentes de Deploy: ex: Canary, Blue/Green, etc. Planejar e executar as estratégias adotadas envolvendo mais de uma equipes como marketing, vendas ou produto. Ela também envolve recursos como balanceadores de carga, implementação de um ciclo para feature flags (se estiver em uso), infraestrutura imutável em alguns casos de uso, etc.

## Como se relacionam de fato? Continuous Integration, Continuous Delivery e Continuous Deployment?

Seguindo a lógica deste texto a relação entre os três seria Continuous Integration, Continuous Delivery como sequência e Continuous Deployment como parte do Continuous Delivery.

![](/images/cd-novo-1.png)

Contudo, essa divisão entre os Continuous é muitas vezes tênue e nem tão fácil distinguir. A uma tendência no mercado de alguns anos de que as etapas de um Pipeline serem representadas como Continuous Delivery, isso se acontece porque ele se alinha naturalmente com as áreas de negócio, com a entrega de valor. Talvez, uma representação melhor seja Continuous Integration e Continuous Deployment envolvidos por Continuous Delivery.

![](/images/cd-novo-2.png)

Revisitando o livro Accelerate, ele mostra como as práticas de Lean Software Development e Continuous Delivery são a base fundamental para diminuir o Lead Time de produtos, Lead Time for Commit, como também criar para círculo virtuoso de aprendizado contínuo. Ele possibilita auditar todas as etapas de um Pipeline de forma transparente e também gerar evidências, assim como testes de conformidade ou aceitação para a disciplina de mudança (Gerência de Mudança ou **C**hange-**A**dvisory **B**oard). Continuous Delivery é o melhor caminho para melhorar desempenho de equipe, entregar valor mais rapidamente, isso não quer dizer que é o caminho mais fácil.

Continuous Deployment se torna crítico em organizações com uma boa implementação de Continuous Delivery, as estratégias de Deploy se tornam críticas para validar testes, experimentações de softwares e produtos. Não trate a estratégia de Deploy como algo somente técnico, é de grande valor para negócio porque possibilita a cultura da experimentação e aprendizado constante para múltiplas equipes para além de nós tecnologistas atuamos. 

**Nota 1**: Esta é uma opinião, não considere como fonte absoluta da verdade. Na dúvida, leia as referências e tenhas as próprias conclusões. ;)

**Referências**:
* [Site - Continuos Delivery](https://continuousdelivery.com/)
* [Livro - Continuous Delivery](https://www.amazon.com.br/Continuous-Delivery-Deployment-Automation-Addison-Wesley-ebook/dp/B003YMNVC0)
* [Livro - Accelerate](https://www.amazon.com.br/Accelerate-Software-Performing-Technology-Organizations-ebook/dp/B07B9F83WM/)
* [Martin Fowler - Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html)