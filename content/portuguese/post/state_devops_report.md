+++
title = "Um review do State of DevOps Report 2017"
date = "2017-06-23T14:07:37-03:00"
description = "Análise dos dados mais relevantes do relatório da Puppet e DORA"
draft = false
tags = ["devops", "puppet", "portugues", "buzzword", "continuous delivery"]
categories = ["devops", "portugues"]
+++
A [Puppet](https://puppet.com/) e [DORA](https://devops-research.com/) liberaram os dados da pesquisa que eles realizam anualmente sobre DevOps nas organizações, o [State of DevOps Report](https://puppet.com/resources/whitepaper/state-of-devops-report) é interessante por trazer informações e conclusões interessantes sobre os diferentes estágios da implantação da cultura DevOps.

Separei alguns pontos que achei mais relevantes, fique a vontade para acrescentar ou corrigir qualquer um deles. De qualquer forma, recomendo uma leitura do documento completo, traz detalhes interessantes e também a metodologia usada no estudo.

#### Percentual baixo de mulheres

Este é um número muito intrigante, por que um percentual tão baixo de mulheres respondeu ao estudo? É o mesmo percentual de [2016](https://puppet.com/resources/whitepaper/2016-state-of-devops-report), no estudo de [2015](https://puppet.com/resources/whitepaper/2015-state-devops-report) mostrou que **33%** das pessoas que responderam a pesquisa daquela ano não trabalhavam com mulheres. Infelizmente o estudo não conseguiu captar a razão de poucas mulheres terem respondido ou mesmo mostrar uma comparação de 2015 até 2017 para identificar se houve um acréscimo de mulheres na TI nesses últimos dois anos.

#### Equipes DevOps são uma realidade

Apesar de ser consensual que DevOps não é uma função de trabalho ou mesmo equipe, a demografia do relatório aponta um crescimento das equipes DevOps desde 2014. Em 2014 era 16% e em 2017 é **27%**. Outras equipes que mais responderam a pesquisa foram Operações de TI ou Infraestrutura; Desenvolvimento ou Engenharia.

**Empresas com equipes DevOps são organizações de alta performance?**

Não necessariamente, lembre-se que muitas organizações criam equipes ou contratam pessoas para serem DevOps porque atualmente é um buzzword. Não quer dizer que é/será um lugar que usa a Cultura DevOps. Se você for fazer uma entrevista para uma vaga DevOps, pergunte sobre a cultura da empresa e da equipe que você irá trabalhar.

#### Liderança é determinante para implementar uma cultura

O relatório identifica que a cultura DevOps tem não teve até então muita coisa elaborada o quanto as lideranças podem facilitar a transformação de uma organização para uma cultura de alta performance. Ele cita 4 tópicos que a liderança transformacional é importante:

* Suportar e estabelecer normas culturais produtivas e de alta confiança.

* Implementar tecnologias e processos que permitem desenvolver a produtividade, reduzindo o tempo de entrega, reduzindo a implantação do código e suportando infraestrutura mais confiáveis.

* Apoiar a experimentação e inovação em equipe, criar e implementar produtos melhores mais rapidamente.

* Trabalhar os silos organizacionais para alcançar o alinhamento estratégico.

Já mencionei algumas vezes no podcast que o [Eriksen Costa](https://twitter.com/eriksencosta) e eu apresentamos sobre como meu passado como gerente de TI e como me transformei de um chefe trollador para um incentivador da equipe. Para mim, nenhuma cultura de alta performance consegue se perpetuar se houver uma liderança tóxica na organização. Gerentes, coordenadores e líderes são importantes para que a cultura DevOps aconteça numa organização. Se não tiver forte cooperação deles, pode-se avançar em muitas coisas do ponto de vista tecnológico, mas nunca terá uma relação franca, criativa e produtiva entre todos.

#### Entrega mais rápidas não refletem em código melhor

Gostei do termo "*[Bad code faster](https://electric-cloud.com/blog/2017/06/top-5-takeaways-2017-state-devops-report/)*" que a [Electric Cloud](https://electric-cloud.com/) usou para destacar a que as organizações de baixa performance estão fazendo deploy mais frequentes mas não necessariamente melhor que antes. O estudo mostra que o tempo de recuperação (MTTR) para voltar um sistema aumentou ao comparar com 2016. Eles (Puppet e Dora) desconfiam que as organizações de baixa performance investiram em aumentar a velocidade, mas não na qualidade do processo. A Electric Cloud aponta para a dificuldade para iniciar uma cultura de teste (Unitários, integração...). Qual a razão para você?

#### Automação é o nirvana mas há dor no caminho

Automação continua sendo um dos pilares para a Cultura DevOps mas o caminho a percorrer das organizações ser tornarem de alta performance não é uma linda estrada asfaltada, reta e plana. O estudo mostra que organizações estão em transição (média performance) tem mais trabalho manual do que as de baixa performance. Ele considera que esse trabalho manual extra é um estágio temporário porque as equipes descobrem uma montanha de débito técnico.


#### Os fatores que contribuem positivamente para Continuous delivery

Pode-se afirmar que Continuous Delivery é fundamental para transformar uma organização. No estudo identificam os seguintes fatores que contribuem:

* Automação de Testes
* Automação de Deploys
* Segurança integrada ao trabalho de entrega de software
* Continuous Integration e desenvolvimento baseado no trunk
* Controle de versão compreensível  

Eles também identificam algumas práticas para o sucesso do Continuous Delivery que uma equipe fizer:

* Fazer mudanças em larga escala no desenho do seu sistema sem a permissão de alguém de fora da equipe.
* Fazer mudanças em larga escala no desenho do seu sistema sem depender de outra equipe para fazer a mudança no sistema deles, ou criar trabalho significativo para outras equipes
* Complete seu trabalho sem precisar de comunicação e coordenação em demasia com as pessoas de outra equipe.
* Deploy e lançamento do produto ou serviço por demanda, independentemente de outros produtos e serviços dependentes.
* Faça a maioria dos testes sob demanda sem exigir um ambiente de teste integrado.
* Execute os deploys durante horário comercial com downtime negligenciado

#### Desenvolvimento baseado no trunk

O estudo mostra que o desenvolvimento de software for baseado no trunk há um ganho estatisticamente considerável ao invés criar branches de longa vida. Há recomendação é seguir as seguintes práticas de desenvolvimento:

* Merge do código no trunk diariamente
* Ter branches ou forks com ciclo de vida bem curto (menos de um dia)
* Ter menos de três branches ativos.

Ao seguir essas práticas as organizações de alta performance têm pouco esforço na integração (algumas horas). As organizações de baixa performance pelo contrário, as equipes ficam alguns dias para fazer o merge.

**Referências**:

- State of DevOps Report 2017: https://puppet.com/resources/whitepaper/state-of-devops-report
- State of DevOps Report 2016: https://puppet.com/resources/whitepaper/2016-state-of-devops-report
- State of DevOps Report 2015: https://puppet.com/resources/whitepaper/2015-state-devops-report
- Top 5 Takeaways from the 2017 State of DevOps Report: https://electric-cloud.com/blog/2017/06/top-5-takeaways-2017-state-devops-report/
