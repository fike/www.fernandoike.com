---
categories: ["portugues", "postgresql", "timbira", "SL", "docker"]
tags: ["portugues", "postgresql", "postgresql brasil", "mailman", "docker"]
date: 2016-01-11T14:28:57-02:00
description: "Estatísticas das listas do PostgreSQL Brasil"
keywords: ["portugues, postgresql, postgresql brasil, mailman, docker"]
draft: false
title: 10 Anos do PGBR - Listas
---
![Logo_PGBR](/images/logo_pgbr.png)

O Telles [lembrou](https://savepoint.blog.br/10-anos-de-pgbr/) dos 10 (17) anos do [PostgreSQL Brasil](https://www.postgresql.org.br/), meus dois centavos são sobre os números das lista de discussão do PostgreSQL Brasil. Desde 2006, as listas de discussão estão hospedados em servidores dedicado.

Um levantamento rápido dos emails das listas até 2015 deu os seguintes números:

- De 2006 à 2015 foram enviados 49.002 emails.
- 2008 foi o ano que mais foi enviado email: 9.322
- 2014 foi ano que menos email foi enviado: 2.523

![Raking_ano](/images/pgbr_emails_2006-2015.png)

A queda de emails nas listas reflete os problemas de instalabilida que ocorrem nos últimos anos (2013-2015). Ela foi um efeito colateral da migração para contêineres (Docker), o Logrotate parava o serviço do Mailman e não conseguia reiniciá-lo. O problema ocorria porque as imagens (de contêiner) baseadas no Debian e derivados alteram a [Policy-rc.d](https://people.debian.org/~hmh/invokerc.d-policyrc.d-specification.txt), a alteração é para que a instalação e/ou atualização de pacotes não reiniciem automaticamente os serviços. O (gambiarra) workaround  foi alterar o script de rotação dos logs, removendo **invoke-rc.d** para **/etc/init.d/comando**.

Desde Agosto de 2015 às listas do PostgreSQL Brasil não tiveram mais problema de disponibilidade, reflexo disso é o aumento de emails nas listas. Também contribuiu para o aumento a conferência PostgreSQL Brasil em Porto Alegre.

![Ranking_2015_mes](/images/pgbr_emails_2015_mes.png)

Para terminar este texto, um ranking dos participantes mais ativos das listas em 2015.

![Ranking_top10_2015](/images/pgbr_top10_2015.png)
