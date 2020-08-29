+++
title = "Devops por onde comecar"
date = "2013-03-30"
draft = false
categories = ["devops", "portugues", "agile", "SL"]
tags = ["devops", "portugues", "agile", "sysadmin"]
+++
O [Guto](http://gutocarvalho.net/)
[publicou](http://gutocarvalho.net/octopress/2013/03/16/o-que-e-um-devops-afinal/)
um excelente texto sobre a origem e concepcão do termo
[DevOps](http://dev2ops.org/2010/02/what-is-devops/). Daqui alguns
tempo, provavelmente, alguém inventará alguma certificação para DevOps
ou formatará o conceito num esquema bem chato.

Enquanto isso (felizmente) ainda não acontece, como você bonitão pode
torna-se um DevOps. Como muitos já disseram, não tem uma fórmula pronta
mas é importante entender que DevOps é uma cultura e como tal não tenha
pressa em se tornar um do dia para noite.

Antes de tudo, vamos falar um pouco de [Sysadmin](https://lopsa.org/).
Muitas das práticas de DevOps são fundamentadas em disciplinas de
Sysadmins. Não que você precise se tornar um Sysadmin mas conhecer um
pouco mais da área ajudará ter um rendimento melhor.

Sysadmin
--------

Um bom Sysadmin deve conhecer (texto levemente modificado do
[original](http://core.eti.br/2010/03/07/para-ser-um-sysadmin/) do
[coredump](http://core.eti.br)):

1.  Sistemas Operacionais e Organização de Computadores (não adianta
    tentar ser um sysadmin sem ter um amplo conhecimento de como o SO e
    Hardware funcionam).

2.  Rede (mesma coisa ali de cima, e aqui estamos falando daquelas
    chatices de TCP/IP, cabeçalhos, window size, mtu e tudo mais, não só
    roteamento).

3.  Programação (tem de saber algum shell script, e mais uma linguagem
    de verdade).

4.  Conceito das linguagens utilizadas no ambiente que vai se
    administrar ([java](http://www.java.com),
    [ruby](http://www.ruby-lang.org), [python](http://www.python.org),
    etc…)

5.  Banco de Dados em geral,
    [NoSQL](http://martinfowler.com/nosql.html),
    [SQL](http://en.wikipedia.org/wiki/SQL), etc. (como eles funcionam,
    transações, locking, particionamento, tuning).

6.  Conceito de virtualização.

7.  Inglês (isso é óbvio).

Diria que isso seria os fundamentos para um bom sysadmin.

Software Livre/Código Aberto e a Cultura DevOps
-----------------------------------------------

Muitas das tecnologias usadas no cotidiano de um DevOps é baseado em
programas que são ou derivam de Software Livre/Código Aberto. Não existe
nenhum impedimento de implantar a cultura DevOps num ambiente
tradicional e de uso de tecnologias de Software Proprietário, é viável
porém o caminho é um pouco mais longo.

Então, se conhecer um ambiente assim, comente logo mais abaixo. ;)

Infraestrutura Ágil
-------------------

Hã? Infraestrutura Ágil? É como Desenvolvimento Ágil
([Scrum](http://www.scrum.org/),
[XP](http://www.extremeprogramming.org/), etc.)? Em parte sim, DevOps
depende de uma mudança cultural na área de infraestrutura Ela está
habituada aos Tickets, Requisições de Mudança, Gerência de Problemas e
outras processos já consolidados.

Uma Infraestrutura Ágil para torna-se realidade necessita de uma mudança
cultural que em muitos casos demora para acontecer por mais diversas
razões (tema para outro texto) e tem muitas formas de realizar. O maior
desafio é como fazer a transição cultural sem que causar o caos.

Inicialmente, usar Kanban já bom início mas use o
[Kanban](http://www.kanbanblog.com/explained/) como substituto de um
sistema de ticket ou incidente. Ele é bom quando usado para gerenciar
partes de projetos ou gerência de problema.

DevOps
------

Num cenário perfeito, uma empresa tem em praticamente toda área de TI a
cultura ágil no cotidiano. Mas é possível implantar a cultura DevOps
mesmo que outras áreas da empresa tenham a cultura tradicional de TI.
Algumas coisas tecnologias que fazem parte do cotidiano.

1.  Orquestração

[Chef](http://www.opscode.com/chef/), [Puppet](https://puppetlabs.com/),
[CfEngine](http://cfengine.com/), [Juju](https://juju.ubuntu.com/),
[Comodit](https://github.com/comodit) e tantos outros são soluções
usadas para gerenciar infraestrutura, deploy, implementar uma
arquitetura escalável, etc. Se não conhece nada na área, comece com
Puppet ou Chef.

1.  Monitoração/Monitoramento

Um Sysadmin já paranóico com monitoramento, num cenário que está usando
a ”*nuvem*” para hospedar as aplicações, monitorar é imprescindível mas monitorará-las
também gera uma grande quantidade de dados. Saber os itens a
serem monitorados bem como os gatilhos (thresholds) torna-se questão de
sobrevivência.

1.  Time de robôs

[Larry Wall](http://www.wall.org/~larry/), criador da linguagem
[Perl](http://www.perl.org/) disse uma vez num livro que tinha preguiça
de repetir as coisas e esse foi um dos principais motivos dele criar a
linguagem. De certa forma isso se aplica também para um Sysadmin/DevOps
pois é parte importante da automação da infraestrutura.

Ah, claro! Cuide bem de seus bots. ;)

1.  StandUp Meet/Comunicação

No ambiente tradicional-corporativo, é muito difícil a área de
infraestrutura reunir-se para conversar sobre tarefas, projetos,
problemas, etc. Principalmente nas empresas com grande contigente na
área de TI.

Fazer reuniões rápidas em que as pessoas troque informações relevantes
sobre o que estão fazendo e que pretende fazer é tão importante como os
tickets, chamados ou ordem de serviços. Elas são importantes para que a
equipe tenha sinergia, empatia e trabalhe com equipe e não um punhado de
indivíduos com a mesma função

1.  Flexibilizar

Tradicionalmente nas empresas tem as conhecidas janelas de deploy das
aplicações ou configurações. Nos casos mais tradicionais as janelas de
deploy estão comprometidas por meses.

Na Cultura Ágil e por conseguinte na Cultura DevOps esqueça disso,
provavelmente terá semanas que terá um dois deploys por dia e em casos
extremos terá centenas de deploy por dia. Isso acontece, principalmente,
em ambientes web e reflete que as aplicações estão eternamente em Beta.
Não que seja ruim, pelo contrário, se as aplicações atingirem a
maturidade é porque o negócio da empresa não esteja tão bom como pensado
ou porque fechou as portas.

Obs. Este texto esta em Beta, volte mais tarde.
