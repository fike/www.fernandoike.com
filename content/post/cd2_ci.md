+++
title = "Continuous Integration Vs Continuous Delivery Vs Continuous Deployment"
date = 2020-07-13T22:50:21-03:00
draft = true
description = "Um revisão sobre Continuous Delivery, Continuous Integration e Continuous Deployment"
categories = [""]
tags = [""]
+++
O senso comum sobre o papel de Continuous Deployment (Implantação Contínua) é de ele ser a automação após testes (geralmente, de aceitação) serem validados,  o artefato segue para implantação para implantação no ambiente de produção numa organização. A forma mais comum de ver é mostrar as etapas de um Pipeline (fluxo de trabalho ou workflow) de desenvolvimento de software com as etapas: Construção, Testes, Integração, Testes de Aceitação e Implantação em produção. A quantidade de etapas e quais etapas envolvidas podem variar a depender do autor, mas é essencialmente representada na figura abaixo.

![](/images/cd_classico.png)

Ao olhar para a figura, o primeiro entendimento que Continuous Deployment seria o ciclo mais completo de automação de um Pipeline, Porque a diferença entre ele Continuous Delivery é apenas a automação da implantação em produção. Olhe novamente para figura, se personificar alguém que tem pouco conhecimento sobre ciclo de desenvolvimento de software, ela irá entender que Continuous Deployment é mais completo dos três porque Continuous Integration é um ciclo parcial porque não contempla a implantação em produção. Continuous Delivery contém todas as etapas que Continuous Deployment, exceto pela implantação de artefato sendo manual.

O que a maioria dos textos que contém imagens semelhantes a figura acima é na realidade representar o Pipeline de forma sequencial. Continuous Integration primeiro, na sequência Continuous Delivery e por fim, Continuous Deployment.

![](/images/cd_classico-2.png)

## Por que automatizar o Pipeline de desenvolvimento de software?

A maior razão para automatizar é ter um processo de construção de uma versão de software (artefato) reproduzível e auditado. Ainda hoje em organizações com baixa maturidade em engenharia de software a construção de um artefato ser manual, assim como os testes e implantação em produção ser manual. Claro, a automação também gera o benefício de diminuir o Lead Time porque o feedback é mais rápido se o artefato está bom o suficiente para ir a produção. 

O Feedback Loop de cada etapa do processo também potencializa a aprendizagem, as políticas de aceitação: cobertura de teste, complexidade de código, integração com outros sistemas, desenvolvimento seguro, etc. mostram para o desenvolvedor o que ele precisa fazer para as novas funcionalidades sejam aceitas no Pipeline. 

Feedback loops acontecem em diferentes métodos, frameworks numa organização, não importa qual é usada, mas sim como é o real aprendizado das equipes envolvidas a cada iteração (e interação) no processo de construção de um artefato de software. 

![](/images/pipeline.png)

A cada iteração e alguma não conformidade em algumas das etapas de um Pipeline, a transparência do processo, ou seja, todos podem olhar porque ocorreu aquela não conformidade e observar o que é feito para tornar aquela(s) funcionalidade(s) tornarem-se em conformidade com as restrições impostas no processo. Sim, a responsabilidade de corrigir é do desenvolvedor e/ou da equipe responsável, contudo, tendo os processo transparentes e auditáveis pode potencializar o aprendizado mais acelerado. 

Há outros benefícios que são abordados brilhantemente nos livros Continuous Delivery e também no Accelerate, por hora, não será aprofundado neste texto.

## Continuous Integration?

O site do Martin Fowler tem uma boa descrição sobre Continuous Integration (tradução livre):

> “... é uma prática de desenvolvimento de software onde os membros de uma equipe integram o trabalho com frequência, usualmente cada pessoa integra diariamente - executando para múltiplas integração por dia. Cada integração é verificada por uma construção automatizada (incluindo testes) para detectar erros de integração o mais rápido possível. Muitas equipes acreditam que esta abordagem reduz de forma significativa problemas de integração e permitir um equipe desenvolver software coeso mais rapidamente.”

Isso é evidenciado num Pipeline automatizado com a construção de um artefato com as modificações realizadas por uma pessoa, no momento que ela envia as modificações para um SCM (Source Code Management). Um serviço de Continuous Integration/Continuous Delivery copia o conteúdo com as modificações realizadas e constrói um novo artefato, seguindo a sequência de etapas configuradas para gerar o artefato, testá-lo e implementá-lo no ambiente de produção (se assim configurado).

## Continuous Delivery?

A melhor definição sobre Continuous Delivery está no site mantido por Jez Humble (tradução livre): 

> “É a capacidade de aplicar as alterações de todos os tipos - incluindo novos recurso, alterações de configuração, correções de bugs e experimentos - em produção ou nas mãos do usuários com segurança e rapidez, de maneira sustentável.”

Esta definição é uma síntese do livro de mesmo nome, escrito por ele por Dave Farley. Importante, não se atenha somente a frase acima, a leitura do livro é recomendada. 

A figura comparativa entre Continuous Integration, Continuous Delivery e Continuous Deployment não é condiz com a descrição acima. Exceto se isolar o fluxo do Continuous Delivery. 

![](/images/cd_classico-3.png)

A automatização de todas etapas de um Pipeline não devem acontecer no dia 1, nem no dia 2. Deve ocorrer, como descrito no site do autor, de maneira sustentável. Conforme evolução da maturidade de cada do processo, avança até a automação da implantação de artefatos em produção.

## Continuous Deployment
Não é só automatizar a implantação em produção como mostrado lá na primeira figura deste texto. Recorrendo novamente ao site do Jez Humble:

> “Continuous Deployment é a prática de liberar toda boa construção de artefato para os usuários”

Atualmente, não é só implementar em produção um artefato para os usuários. Envolve em planejar em quais das diferentes estratégias existentes de Deploy, ex: Canary, Blue/Green, etc. Também envolve mais de uma equipe, muitas vezes envolve outros papéis e equipes como marketing, vendas ou produto.
Continuous Deployment também envolve recursos como balanceadores de carga, implementação de um ciclo para feature flags (se estiver em uso), infraestrutura imutável em alguns casos de uso, etc. 

## Como se relacionam de fato? Continuous Integration, Continuous Delivery e Continuous Deployment?

Seguindo a lógica deste texto a relação entre os três seria Continuous Integration, Continuous Delivery como sequência e Continuous Deployment como parte do Continuous Delivery.

![](/images/cd-novo-1.png)

No entanto, essa divisão entre as partes não é tão fácil de distinguir. O alinhamento dos processos em torno do conceito de Continuous Delivery com negócio o faz como um envolver outros conceitos como parte dele. Uma representação melhor seja Continuous Integration e Continuous Deployment envolvidos por Continuous Delivery.

![](/images/cd-novo-2.png)

Revisitando o livro Accelerate, ele mostra como as práticas de Lean Software Development e Continuous Delivery são a base fundamental para diminuir o Lead Time de produtos, Lead Time for Commit, como também para círculo virtuoso de aprendizado contínuo. Ele possibilita auditar todas as etapas de um Pipeline de forma transparente e também gerar evidências, assim como testes de conformidade ou aceitação para a disciplina de mudança (Gerência de Mudança ou **C**hange-**A**dvisory **B**oard). Continuous Delivery é o melhor caminho para melhorar desempenho de equipe, entregar valor mais rapidamente, isso não quer dizer que é o caminho mais fácil.

Continuous Deployment se torna crítico em organizações com uma boa implementação de Continuous Delivery, as estratégias de Deploy se tornam críticas para validar testes, experimentações de softwares e produtos. Não trate a estratégia de Deploy como algo somente técnico, é de grande valor para negócio porque possibilita a cultura da experimentação, aprendizado rápido para além da área de onde nós tecnologistas atuamos.

**Nota** 1: Esta é uma opinião, não considere como fonte absoluta da verdade. Vá para as referências para saber mais.
