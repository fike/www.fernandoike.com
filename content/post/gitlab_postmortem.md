+++
title = "O Postmortem da Gitlab"
description = "Análise e lições do Postmortem da Gitlab"
categories = ["devops", "portugues", "sre"]
tags = ["devops", "portugues", "sre", "blameless", "postmortem", "gitlab", "netflix", "google", ]
draft = false
date = "2017-02-13T15:34:54-02:00"

+++
Relatórios Postmortem públicos são de grande valor para todos que querem aprender a partir de incidentes já ocorridos. De certa forma, eles são parecido com os relatórios sobre acidentes de avião. Identifica-se a(s) causa(s) do acidente e quais a recomendações para que não ocorra novamente. A diferença entre um relatório de um acidente de avião e postmortem de TI é que o segundo não irá culpar pessoas nominalmente (**blameless**) pelo problema, mas indicar o que deve ser feito do ponto de vista de processo, arquitetura de software, etc.

Blameless é muito importante para cultura **DevOps** e também para **SRE**, ela possibilita criar um ambiente na organização analisar um incidente ou um bug sem culpar pessoas pelo problema e identifica a causa raiz; como também as lições aprendidas para que não ocorra novamente. Algumas empresas com as quais conversei sobre DevOps fazem relatórios Postmortem mas os mantém em privado, contudo, existe um movimento cada ver maior nas empresas do exterior tanto  em tornar seus relatórios públicos como forma de explicar para os clientes porque aconteceu um incidente, como também as lições aprendidas para que outros não tenham o mesmo tipo de problema.

O livro SRE do Google tem um capítulo específico ([Postmortem Culture: Learning from failure](https://landing.google.com/sre/book/chapters/postmortem-culture.html)), outro texto interessante sobre **Postmortem** e **Blameless** é do [John Allspaw](https://twitter.com/allspaw) ([Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)). Ao menos para mim, [um dos mais interessantes relatórios Postmortem](https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/) é do [Gitlab](https://about.gitlab.com/), eles tiveram uma indisponibilidade no banco de dados no dia 31 de janeiro de 2017. Abaixo algumas notas minhas sobre o incidente.

A causa raiz foi executar o "***rm -rf***" no servidor de banco de dados ([PostgreSQL](https://www.postgresql.org/)) principal, o objetivo ao rodar o comando no servidor de banco secundário era limpar a base e reiniciar a replicação entre eles que tinha parado. A replicação parou por causa de uma sobrecarga, o servidor primário removia os WAL segments antes que o servidor secundário pudesse aplicá-los.

A recuperação do backup foi demasiadamente lenta (18 horas), isso porque a recuperação via backups feitos pelo pg_dump (9.2) foram realizado na versão diferente do banco em produção (9.6). A outra forma de tentarem recuperar foi usando os snapshot do LVM e também dos discos do Azure, a demora ocorreu porque os discos no serviço padrão são lentos como a maioria dos IaaS. A não ser que seja contratado discos mais rápidos (e caros) ou adote baremetal.

Antes de você tirar conclusões a partir daqui, recomendo que leia o relatório do Gitlab e depois comente, eles detalham tudo que aconteceu e o que estão fazendo para melhorar. No relatório, eles usam o **5 Whys** (**5 porquês**) para identificar porque ocorreu a indisponibilidade do servidor de banco de dados e porque demorou para recuperar o serviço. [5 Whys](http://www.toyota-global.com/company/toyota_traditions/quality/mar_apr_2006.html) é uma técnica interrogativa [iterativa](https://pt.m.wiktionary.org/wiki/iterativo) para identificar a causa raiz de um defeito, é parte do [Toyota Production System](http://www.toyota-global.com/company/vision_philosophy/toyota_production_system/).

Especificamente sobre PostgreSQL, existem muitas formas de replicação que poderiam evitar ou minimizar um incidente deste tipo. Este não é o ponto deste texto (quem sabe num outro), uma das formas de melhor rapidamente a resiliência de um serviço é através do Game Day, identificando gargalhos e problemas de disponibilidade nos serviços através de testes de carga/resiliência. Este processo também é chamado de Engenharia de resiliência, [Jesse Robins](https://twitter.com/jesserobbins) falou sobre isso na Usenix Conference: *[GameDay: Creating Resiliency Through Destruction](https://www.youtube.com/watch?v=zoz0ZjfrQ9s)*

GameDay é bem interessante, tem um estudo de caso em que Jesse Robbins, Kripa Krishnan, John Allspaw, e Tom Limoncelli tem um estudo de caso em que discutem sobre ele em [Resilience Engineering: Learning to Embrace Failure](https://queue.acm.org/detail.cfm?id=2371297). Em trecho da conversa Jesse Robins comenta:

> ... você não pode escolher se vai ter ou não falhas, elas irão acontecer, não importa o que você faça, em muitos casos você pode escolher quando irá aprender as lições.

Já participei de testes similares para duas instituições financeiras. Na ocasião, o objetivo era melhorar o processo de mitigação de ataques DDoS, para isso eram realizadas simulações de diversos tipos de ataques DDoS. A cada teste era identificado um equipamento, serviço, processo ou sistema que deveria ser revisto pois algum tipo de ataque não era mitigado. Após vários testes, essas instituições sofreram vários ataques DDoS reais que foram mitigados sem grande impacto para os clientes delas.

**Referências**:

**Gitlab** - **Postmortem of database outage of January 31**:
https://about.gitlab.com/2017/02/10/postmortem-of-database-outage-of-january-31/

**Livro - Google SRE**: https://landing.google.com/sre/book/chapters/postmortem-culture.html

**John Allspaw** - **Blameless PostMortems and a Just Culture**: https://codeascraft.com/2012/05/22/blameless-postmortems/

**Jesse Robins** - **GameDay: Creating Resiliency Through Destruction** - https://www.youtube.com/watch?v=zoz0ZjfrQ9s

**Resilience Engineering**: **Learning to Embrace Failure**: https://queue.acm.org/detail.cfm?id=2371297

 **5 Whys**: http://www.toyota-global.com/company/toyota_traditions/quality/mar_apr_2006.html

**Google Compute Engine Incident #16007**:   https://status.cloud.google.com/incident/compute/16007?post-mortem

**Netflix - Post-mortem of October 22,2012 AWS degradation**: http://techblog.netflix.com/2012/10/post-mortem-of-october-222012-aws.html
