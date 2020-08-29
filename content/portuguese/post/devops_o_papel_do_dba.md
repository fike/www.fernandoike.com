+++
categories = ["devops", "portuguese"]
date = "2017-05-10T09:56:32-03:00"
description = "Uma versão da apresentação sobre DBA e DevOps no DBA Brasil 2.0"
draft = false
tags = ["devops", "dba", "data scientist", "release", "automacao"]
title = "DevOps: O novo papel do DBA"

+++
Antes de mais nada, obrigado Fabrízio e a [Timbira](https://www.timbira.com.br/) pela oportunidade de participar do evento como co-palestrante!

[Fabrízio Mello](https://twitter.com/fabriziomello) e eu apresentamos no [DBA Brasil 2.0](https://www.dbabr.com.br/dbabrasil2) como a cultura **DevOps** está mudando o papel do DBA, os slides da apresentação estão no [Slideshare](https://www.slideshare.net/fabriziomello/dba-brasil-20-como-o-papel-e-atividades-de-dba-ficam-no-contexto-da-cultura-devops) e este texto é uma minha reflexão da palestra. Antes de discorrer sobre como a cultura DevOps está modificando o papel do DBA nas organizações, deixa tentar fazer uma definição das atividades clássicas do DBA.

## O DBA 1.0

O **Database Administrator** (**DBA**), no geral, tem suas as atividades vinculadas a área de operações de TI (Infraestrutura) com a responsabilidade de manter os bancos de dados online com bom desempenho e continuamente. Um profissional DBA (geralmente) migra de outras áreas como Desenvolvimento ou mesmo de outras funções da área de Operações, isso ocorre por interesse dele ou porque era o profissional que melhor sabia lidar com modelagem de dados, construção de consultas SQL.

Genericamente, podemos "*classificar*" as principais atividades do DBA como:    

- Planejar, instalar e configurar um Banco de dados (Oracle, SQL Server, PostgreSQL, etc.)
- Arquitetura e criação de banco de dados
- Arquitetura e implantação de Alta Disponibilidade e Disaster Recovery para cada banco de dados
- Monitoramento e manutenção do banco de dados
- Performance Tuning
- Segurança dos Banco de Dados (permissões de acesso, criptografia, patches, etc.

O fato do DBA ser o principal responsável por manter os dados da empresa e como as informações contidas nos bancos dados são vitais para a própria sobrevivência da empresa, o DBA acaba assumindo o papel do guardião das informações da empresa. Isso, de certa maneira, o empodera extraoficialmente e faz sua opinião ser a última palavra quando se discute uma atualização de sistema ou quando aplicar um patch de segurança no sistema operacional onde o banco de dados está sendo executado.

O setor de banco de dados se torna para casos como acima mencionado um mini silo dentro do silo de Operações de TI (Infraestrutura), assim como outros setores como administração de rede ou sistemas também são mini silos. O fato curioso é que um DBA usa o conhecimento em desenvolvimento para criar Store Procedures, como também conhecer Sistema Operacionais e administração de sistemas para fazer Performance Tuning de um banco de dados. Portanto, a função DBA ela já híbrida (Dev/Ops) naturalmente.

### Exemplo do cotidiano do DBA tradicional

Alguns anos atrás e num passado distante, trabalhei para uma empresa que tinha o ERP rodando num banco de dados do tipo SQL. Todo mês a folha de pagamento não fechava corretamente e o fornecedor do ERP tinha que ajustar manualmente para que os empregados recebem o salário com os valores corretos. O DBA passava dias ajudando os analistas do fornecedor do ERP a dar umas marretadas para a folha de pagamento rodar corretamente, ele não comentava sobre suas atividades ou decisões sobre os bancos de dados e quando alguém perguntava ele respondia genericamente. O banco de dados do ERP era uma verdadeira caixa preta, ninguém além dele sabia de fato o que tinha lá.

Passado alguns meses o fornecedor do ERP recomendou que fizéssemos uma grande atualização do ERP pois iria dar um ganho significativo de desempenho. Pois bem, durante meses as atividades foram planejadas e executadas até chegar o dia da virada, o meu chefe decidiu tirar férias e me deixou como responsável pela área. Eu acompanhava de longe o projeto do ERP porque não tinha atividades diretas, meu chefe dizia que estava tudo certo com o projeto e (eu) só tinha que acompanhar a virada. Este foi minha primeira aventura como líder de equipe, realmente acreditei que seria fácil cobrir as férias do meu chefe...

No meu segundo dia (no lugar do chefe) estávamos na reunião de alinhamento e o fornecedor do ERP diz que está tudo certo para rodar a folha de pagamento no sistema novo e o que o antigo ia ser mantido em paralelo. Caso ocorresse algum problema no novo, seria usado o velho. A empresa tinha contratado um novo DBA porque a o antigo tinha ido trabalhar em outro lugar, o DBA pergunta por que as chaves estrangeiras estavam desligadas no novo ERP. O silêncio toma conta da sala e por alguns segundos as pessoas entreolhavam esperando que alguém dissesse alguma coisa. Um dos analistas diz que o motivo é que na folha de pagamento mais antiga era em Cobol e ao migrar para o ERP com banco de dados SQL desligou as chaves estrangeiras porque estava dando pau. Portanto, desligou para poder migrar logo pois o servidor do Cobol estava na UTI e não tinha mais como manter no ar.

Mais alguns segundos de silêncio ensurdecedor. Bom, discutimos algumas alternativas, mas ninguém tinha convicção de adotá-las. O fornecedor do ERP queria manter o cronograma e rodar no novo sistema, alguns analistas queriam manter no velho ERP e outros mais radicais queriam ressuscitar a velha folha de pagamento em Cobol. A solução na época foi fazer um war-room até conseguir rodar o ERP novo de forma consistente, mas a folha de pagamento daquele fatídico mês e o 13o foram rodados em numa planilha Excel.

Foram necessários mais alguns meses para conseguir rodar a folha de pagamento no ERP novo e também aplacar a fúria do departamento de RH e do financeiro até eles usarem o novo sistema. Esta foi a primeira lição da importância de compartilhar conhecimento.

## O impacto de muitos deploys por dia

Houve um aumento significativo de deploys com a adoção do [Agile](https://agilemanifesto.org/), [Lean](https://www.lean.org.br/o-que-e-lean.aspx) e DevOps nas empresas. Os deploys que aconteciam algumas vezes no ano mudou para muitos deploys por dia, num evento do [Meetup Docker São Paulo](meetup.com/Docker-Sao-Paulo/) foi relatado por uma empresa que eles realizam até **90 deploys por dia**. Uma das consequências do aumento de releases dos sistemas é que o DBA precisa estar mais próximo da equipe de desenvolvimento para ajudar na arquitetura e atualização dos sistemas. Uma segunda consequência é acompanhar o monitoramento mais de perto para identificar problemas de desempenho dos bancos dados. Uma terceira consequência é o aumento massivo dos dados a serem gerenciados, forçando algumas empresas a criar uma nova estrutura no organograma da TI para atender a demanda de gerenciar a quantidade massiva de informações geradas pela empresa. Esta nova vertical não tem um nome muito bem definido, em alguns lugares ela será batizada como Data Scientist, em outras como Big Data.

### O DBA 2.0

Até o ano passado eu pensava que o DBA era uma profissão em extinção, mas estava equivocado. O DBA que tratar os banco de dados como parte do seu reinado ou seja, como um mini silo dentro do silo de infraestrutura, este sim estará correndo risco de ser extinto. Este novo perfil do DBA ("2.0") tem características que vão além de simplesmente gerenciar de banco de dados, consultas SQL, índices, etc. Essas características tornam o perfil do DBA mais genérico porque ocorre uma maior interação com diversas equipes e tecnologias. Portanto, ao contrário que possa pensar na extinção da função do DBA, ocorrer um papel de destaque porque o gerenciamento das informações nos banco de dados é mais crítico na Cultura DevOps.

Os novos conhecimentos vão desde aprender novas **Linguagens de Programação**, **Automação e Deployment**, **Release Engineering**, **QA (Testes)**, **Continuous Delivery**, etc. Algumas das atividades deste novo perfil do DBA são similares ao perfil 1.0, contudo há novas atividades que estão relacionadas a cultura DevOps:

- Planejamento
- Construção/Criação
- Testes de QA
- Performance Tuning
- Code Review
- Testing
- Automação de Release
- Monitoramento/Discovery

### Métodos e estratégias de Deploy

Há muitos textos sobre Continuous Delivery, estratégias e métodos de deploy. Mas não há muita coisa sobre Deployment e banco de dados. O Fabrízio contou na apresentação no DBA Brasil 2.0 um caso de migração de 4 bilhões de registros, ao perceberam que não iriam conseguir migrar num único deploy, eles criaram um script para ir migrando em pequenos lotes para fazer a migração em alguns dias e ao fim virar a chave da aplicação para usar o banco de dados já com os dados migrados.

Essa abordagem não sem encaixa em nenhuma das estratégias mais comuns, por isso a importância do DBA se envolver com a equipe de desenvolvimento para trabalharem em conjunto. Neste cenário torna-se necessário o DBA conhecer métodos de Deployment relacionados aos bancos de dados como: Scripts SQL, DACPAC, ferramentas de automação de banco ([Datical](https://www.datical.com/), [DBMaestro](https://www.dbmaestro.com/), [Redgate](https://www.red-gate.com/), etc.). Também é importante conhecer as estratégias: [Canary Release,](https://martinfowler.com/bliki/CanaryRelease.html) Rolling Release, [Blue/Green](https://www.martinfowler.com/bliki/BlueGreenDeployment.html), etc.

Ressaltando que não existe bala de prata, uma única solução, método ou estratégia de Deployment resolverá todos os problemas, cada aplicação ou problema poderá ter uma melhor solução de forma específica. Não esquecendo também que as boas práticas em administração de banco de dados continuam fortemente recomendas, acrescentando algumas coisas novas como **versionamento dos metadados**, [teste unitário](https://pgtap.org/) e **automação de banco da dados**.

Outras coisa interessantes para um DBA conhecer são: [Feature Toggle](https://martinfowler.com/bliki/FeatureToggle.html), [Continuous Delivery](https://www.grupoa.com.br/livros/engenharia-de-software-e-metodos-ageis/entrega-continua/9788582601037) (obviamente), [Brownfield/GreenField](https://www.donnfelker.com/software-development-greeenfield-vs-brownfield/) e [System Thinking](https://watersfoundation.org/systems-thinking/definitions/) ([1st Way to DevOps](https://itrevolution.com/devops-culture-part-1/)).

**Referências**:

- [The Phoenix Project](https://en.wikipedia.org/wiki/The_Phoenix_Project_(novel))
- [CD for DBs: Database Deployment Strategies](https://www.youtube.com/watch?v=hLQAQlwY6-k&feature=youtu.be)
- [DBA Role Shift in a DevOps World](https://www.youtube.com/watch?v=R4XJK_kTKIM)
- [Automating the Database: A Win-Win for DBAs and DevOps](https://www.infoq.com/articles/dba-devops-source-control)
- CAMS - https://itrevolution.com/devops-culture-part-1/
[10+ Deploys Per Day](https://www.youtube.com/watch?v=LdOe18KhtT4)
