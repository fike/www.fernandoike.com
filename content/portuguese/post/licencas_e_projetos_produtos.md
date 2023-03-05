+++
title = "Licenças de Software e impacto numa stack de tecnologia"
date = 2021-02-02T09:35:09-03:00
draft = false
description = "Um reflexão sobre o impacto de empresas mudarem a licença do tipo Open Source para SSPL"
categories = ["licenças", "opensource", "portuguese"]
tags = ["licenças", "opensource", "portuguese", "elastic", "mongodb", "aws"]
+++
!["folhas com descrição de uma lei"](/images/binding-contract-948442_640.jpg)

As decisões sobre quais tecnologias, frameworks e/ou plataformas que serão base do desenvolvimento de produtos e serviços muitas vezes não são racionais. Elas são fortemente influenciadas por gosto pessoal, buzzwords, etc.

Isso é evidente quando as pessoas nas funções de liderança decidem por tecnologia A ou B, muitas vezes a decisão é fortemente influenciada pelo sucesso de projetos anteriores, recomendação de outras pessoas ou parceiros comerciais. Não há nenhum problema em tomadas de decisão assim, desde que tenha claro as limitações de cada tecnologia versus as condições da equipe de adotar a tecnologia definida na decisão.

Um exemplo é quando eu estava na posição de gestor (CTO) de uma startup na área de educação. Uma das minhas responsabilidades era criar uma equipe de tecnologia para desenvolvimento de uma plataforma para a rede de escolas desta startup.

A stack para desenvolvimento seria [Python](https://www.python.org/), especificamente [Django](https://www.djangoproject.com/) como backend, [PostgreSQL](https://www.postgresql.org/) como banco de dados e como FrontEnd um dos três mais  conhecidos (ao menos por mim), [Angular](https://angular.io/), [React](https://reactjs.org/) ou [Vue](https://vuejs.org/). Como meu conhecimento desses frontends eram muito básico, eu não era capaz de decidir por qual deles usar, a decisão seria das pessoas de front contratadas.

A escolha por Python, Django ([REST Framework](https://www.django-rest-framework.org/)) foi porque Python é uma linguagem de programação com uma curva de aprendizado mais baixa (não quer dizer mais fácil) comparada à outros frameworks, a popularidade da linguagem e consequentemente maior possibilidade de contratar pessoas com algum conhecimento.

Outra parte importante seria o uso de containers desde o início do projeto. As primeiras versões rodam em containers ([Docker](https://www.docker.com/)) nas VMs do IaaS contratado, isso posteriormente foi migrado para [Kubernetes](https://kubernetes.io/), a razão principal disso é gerar cada artefato contido num container, padronizando a construção do artefato e rollout dele nos ambientes de homologação e produção.

O PostgreSQL é um banco versátil para diferentes usos, os principais provedores de Cloud tem oferta de serviço gerenciado dele  e os ORMs ([SQLAlchemy](https://www.sqlalchemy.org/) e [Django ORM](https://docs.djangoproject.com/en/3.1/topics/db/queries/)) funcionam bem também. Na startup anterior, ele foi utilizado com armazenamento de uma das plataformas desenvolvidas utilizando [Event Sourcing](https://microservices.io/patterns/data/event-sourcing.html) (valeu [Mário Idival](https://twitter.com/marioidival) por implementar!).

Analisando o exemplo que citei, as decisões sobre quais tecnologias seriam utilizadas tinha até bons argumentos, não é possível afirmar que não havia algum viés. Containers como base dos artefatos gerados, PostgreSQL como banco de dados foram decisões tecnológicas baseadas em implantações de sucesso em experiências anteriores.

Reforçando, não há problema em tomar decisões assim, cabe ponderar junto com as pessoas que irão desenvolver porque utilizar aquelas tecnologias e identificar potenciais limitações de cada tecnologia não só do ponto de vista técnico, mas também na capacidade da equipe aprender lidar com elas e olhar para outras tecnologias sem estigma da obrigação de aprender “tudo de novo”.

Há outro aspecto que é pouco abordado nas decisões de quais tecnologias serão adotadas, mas com a mudança das licenças do MongoDB e ElasticSearch despertou um interesse maior sobre as licenças de software.

**Observação** - A análise aqui é uma opinião, não sou advogado. Não use o conteúdo abaixo como referência, consulte uma empresa especializada no assunto.

Na startup escolhemos a maior parte da nossa stack base estava com licença do tipo permissiva (BSD): PostgreSQL, Django e Django REST. Python ([PSF License Agreement](https://docs.python.org/3/license.htm)) e Psycopg2 ([LGPL-3](https://www.psycopg.org/license/)) são “derivadas” da [GPL-2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html) e [GPL-3](https://www.gnu.org/licenses/gpl-3.0.en.html). React e [Next.js](https://nextjs.org/) usam [MIT](https://github.com/vercel/next.js/blob/canary/license.md) como licença e a maioria das bibliotecas de dependência dos projetos desenvolvidos usavam [BSD](https://opensource.org/licenses/BSD-3-Clause), MIT ou [Apache2](https://opensource.org/licenses/Apache-2.0).

ElasticSearch foram considerado algumas vezes como parte da stack, mas se fosse iniciar no dia de hoje enquanto escrevo pensaria duas vezes em considerar:

#### 1. O ElasticSearch não está sob uma licença Open Source

Sempre que possível é preferível (para mim) adotar tecnologias com licença considerada Open Source e com uma governança transparente. Isso possibilita um ambiente de colaboração tecnológica e econômica incrível, um bom exemplo são [os projetos mapeados](https://landscape.cncf.io/?license=open-source) pela [CNCF no seu Landscape](https://landscape.cncf.io/) tem um valor de mercado estimado em **10,65 trilhões de dólares**.

A licença [SSPL](https://www.mongodb.com/licensing/server-side-public-license) [não é considerada](https://opensource.org/node/1099) Open Source pela  [OSI](https://opensource.org) (Open Source Initiative).

#### 2. Quebra do ecossistema e usuários são clientes a partir da 7.11

Um ecossistema robusto como criado em torno do ElasticSearch permitiu que empresas crescessem em torno como [Logz](https://logz.io/blog/open-source-elasticsearch-doubling-down/), [CrateDB](https://crate.io/a/cratedb-doubling-down-on-permissive-licensing-and-the-elasticsearch-lockdown/
) e [Aiven](https://aiven.io/press/aiven-statement-on-license-changes-for-elasticsearch) está sendo quebrado por conta da mudança da licença.

Um ecossistema em torno de um projeto opensource contém usuários, clientes, parceiros comerciais, [coopetidores](https://en.wikipedia.org/wiki/Coopetition
) (colaboradores + competidores), voluntários, etc. Ao adotar uma licença como SSPL está eliminando do ecossistema os coopetidores e muitos usuários.

Não é só Elastic que mudou para SSPL, [MongoDB](https://www.mongodb.com/licensing/server-side-public-license
) foi o pioneiro nesse movimento e no ano passado [foi o Graylog](https://www.graylog.org/post/graylog-v4-0-licensing-sspl) que também mudou.

Claro, é [compressível](https://www.elastic.co/blog/why-license-change-AWS) as razões da mudança na licença, mas não é uma questão do tipo: [somos bons e eles são maus](https://www.zdnet.com/article/elastic-changes-open-source-license-to-monetize-cloud-service-use/).

## Qual licença é a melhor então?

Sabe aquela resposta padrão de consultor? “Depende”...

### Enquanto consumidor de tecnologia

Acompanhe o que os desenvolvedores (pessoas e/ou empresas) estão pensando sobre o futuro do projeto que é base da stack de onde trabalha. Mudanças assim não chegam de uma hora para outra.

### Enquanto consumidor mas também desenvolvedor de tecnologia

Vale o mesmo do cenário acima mas com um ponto importante a acrescentar. Se você ou sua organização quer colaborar com algum projeto, veja como é o processo de governança deles. Os projetos incubados em fundações como CNCF ou Apache Foundation tem um modelo claro de governança.

### Enquanto desenvolvedor de tecnologia

A licença do projeto deve estar relacionada ao modelo de negócio que a empresa pretende ter. Para todo tipo de licença Open Source há casos de sucesso, segue alguns exemplos:

* Canvas é um LMS com a licença AGPL desenvolvido pela Instructure
* NextJS é um “React Framwork” com a licença MIT desenvolvido pela Vercel
* MariaDB é um banco de dados com a licença GPL-2  desenvolvido pela MariaDB
* PostgreSQL é um banco de dados com a licença BSD

Se quer usar na sua stack alguma projeto que está sob a licença SSPL é claro que deve usar mas considere que não é de fato, Open Source. 😉

## Referências

* [Vicky Brasseur - Elasticsearch and Kibana are now business risks](https://anonymoushash.vmbrasseur.com/2021/01/14/elasticsearch-and-kibana-are-now-business-risks)
* [Elastic - Amazon: NOT OK - why we had to change Elastic licensing](https://www.elastic.co/blog/why-license-change-AWS)
* [MongoDB - SSPL](https://www.mongodb.com/licensing/server-side-public-license)
* [Percona - Why is MongoDB’s SSPL Bad For You?](https://www.percona.com/blog/2020/06/16/why-is-mongodbs-sspl-bad-for-you/)
* [Graylog - Graylog v4.0 Licensing SSPL](https://www.graylog.org/post/graylog-v4-0-licensing-sspl)
* [OSI - The SSPL is Not an Open Source License](https://opensource.org/node/1099)
* [CNCF - Landscape - Open Source](https://landscape.cncf.io/?license=open-source)
* [Aiven statement on license changes for Elasticsearch](https://aiven.io/press/aiven-statement-on-license-changes-for-elasticsearch)
* [Zdnet - Elastic changes open-source license to monetize cloud-service use](https://www.zdnet.com/article/elastic-changes-open-source-license-to-monetize-cloud-service-use/)
* [CrateDB Doubling Down on Permissive Licensing and the Elasticsearch Lockdown](https://crate.io/a/cratedb-doubling-down-on-permissive-licensing-and-the-elasticsearch-lockdown/)
* [Logz - Truly Doubling Down on Open Source](https://logz.io/blog/open-source-elasticsearch-doubling-down/)
* [Coopetition](https://en.wikipedia.org/wiki/Coopetition)
* [Treinamento Linux Foundation - Open Source License for Software Developers](https://training.linuxfoundation.org/training/open-source-licensing-basics-for-software-developers/)
