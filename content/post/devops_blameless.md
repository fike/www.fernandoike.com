+++
title = "Blameless: A culpa não é sua"
date = 2017-08-21T12:12:12-03:00
draft = false
description = "Primeira parte da versão escrita do palestra sobre Blameless no DevOpsDays Porto Alegre de 2017."
categories = ["devops", "blameless", "lean", "portugues", "agile"]
tags = ["devops", "blameless", "agile", "lean", "portugues", "google", "chaos"]
+++
Você já trabalhou ou trabalha numa organização que pune o erro de alguma forma? Punir o erro não necessariamente é demitir alguém, a punição pode ocorrer de diversas formas: um olhar velado de reprovação, rádio peão, piadas/gozações da situação, etc. A aviação civil tem bons exemplos de identificar analisar as causas de um acidente aéreo, na maioria dos casos tenta-se identificar a(s) causa(s) de um acidente área olhando o todo, não apenas o último erro que "causou" o acidente.

Um caso interessante (e muito triste) para analisar é o do acidente (2007) do avião da TAM no aeroporto de Congonhas em São Paulo. Um avião vindo de Porto Alegre não conseguiu parar ao pousar e colidiu num prédio do outro lado do aeroporto. Um dos órgãos governamentais [apontou](http://sao-paulo.estadao.com.br/noticias/geral,pf-culpa-somente-pilotos-no-acidente-da-tam-em-2007,458242) como causa do acidente os pilotos, mas ao olhar tudo como um processo/sistema complexo verá que foram um conjunto de coisas contribuíram para o acidente e muitas [medidas](http://www.bbc.com/portuguese/brasil-40539541) foram tomadas para evitar que acontecesse um acidente como aquele. O [relatório](http://www2.anac.gov.br/arquivos/RF3054.pdf) do [Cenipa](http://www2.fab.mil.br/cenipa/) não aponta qual a causa mas faz uma série de recomendações que se olhar conjunto, elas podem ter formado uma [tempestade perfeita](https://www.grammarphobia.com/blog/2008/05/the-imperfect-storm.html).

Ainda é muito comum no mundo da Tecnologia da Informação procurar/encontrar/culpados (humanos) por uma falha de um sistema e em caos nem tão extremos, a demissão dos mesmos. Quando isso acontece ou quando achamos que isso irá acontecer, a reação instintiva da nossa é tentar se proteger do perigo (da demissão) e tratamos de fazer as nossas atividades com cautela ou com o conservadorismo excessivo. Mesmo que a missão da organização esteja descrita como audaz, descontraída, etc. A cultura da organização terá o medo como base para as atividades e as pessoas tentarão se exporem menos possível como mecanismo de defesa. John Allspaw chama situação como "[Ciclo de Culpa](https://codeascraft.com/2012/05/22/blameless-postmortems/)" num post sobre como a cultura Blameless é aplicada na Etsy:


1. *Engenheiro tomam atitude e contribuem para uma falha ou acidente.*
2. *Engenheiro é punido, envergonhado, culpado ou reprimido.*
3. *Reduz a confiança entre engenheiros e a gerência fica procurando alguém como bode expiatório.*
4. *Engenheiros ficam em silêncio sobre detalhes de ações/situações/observações, resultando na engenharia de "Cover-Your-Ass" (pelo medo de punição).*
5. *Gerentes tornam-se menos conscientes e informados sobre o desempenho do trabalho do dia a dia, engenheiros se tornam menos educados na espreita ou condição latente para falha devido ao silêncio mencionado no passo* **#4**.
6. *Erros tornam-se mais prováveis, condição latente para eles não serem identificadas devido ao passo* **#5**.
7. *Repete a partir do passo* **#1**

Uma técnica muito comum em lugares que "aplicam" é o apontar o culpado com o dedo, principalmente em reuniões logo após um incidente, esta técnica é muito comum em ambientes em que as pessoas sente que estão trabalhando o tempo todo com a guilhotina apontada para o pescoço. [Sidney Dekker](http://sidneydekker.com/) chama isso de "A teoria da maçã podre" no livro "[The Field Guide to Understanding Human Error](https://www.amazon.com/Field-Guide-Understanding-Human-Error/dp/0754648265)":

> Reprimir as maçãs podres pode parecer uma solução rápida e gratificante, mas é como fazer xixi nas calças. Você sente aliviado, talvez mesmo até agradável e aquecido por algum tempo, mas depois fica frio e desconfortável. E você parece um idiota.

### O erro humano e Sistemas Complexos

A solução de apontar o culpado (humano) só transfere a culpa para quem provavelmente é o menos culpado, em organizações de alta performance a abordagem é ver um incidente como uma falha além de um erro um humano, considerando todas relações, interações e reações de forma abrangente como um **Sistema Complexo**. Isso possibilita identificar várias pequenas coisas nos processos, sistemas e procedimentos que podem ser alteradas para evitar que aquele incidente ocorra novamente.

Este olhar mais abrangente se enquadra em Sistemas Complexos. Segundo [o pai dos burros digital](https://en.wikipedia.org/wiki/Complex_systems#Overview):

> Um sistema complexo é um sistema composto de muitos componentes no qual podem interagir entre si. Em muitos casos é usado para representar como um sistema em rede onde os nós representam os componentes e os links suas interações. Exemplos de sistemas complexos são o clima da Terra, organismos, o cérebro humano, organizações econômicas e sociais (como cidades), um ecossistema, uma célula viva e ultimamente o universo inteiro.

>Sistemas complexos são sistemas cujo o comportamento é intrinsecamente difícil de modelar devido as dependências, relacionamentos, interações entre as partes ou entre um determinado sistema e seu ambiente.

O C do [ICE](https://radar.oreilly.com/2015/01/devops-keeps-it-cool-with-ice.html) em DevOps é a representação de Sistemas Complexos. Dave Zwieback, o autor do acrônimo explica a relação de DevOps e Sistemas Complexos em "*DevOps keeps it cool with ICE*":

> A grande razão que DevOps veio existir é porque nós estamos agora trabalhando com (e em) sistemas complexos e adaptativos, o qual não pode ser abordado de maneira simplista, linear ou casual. De fato, eles estão quase sempre além da habilidade humana para compreender - sistemas complexos funcionam (e quebram) não pode prevista baseado em experiências passadas. Sistemas complexos estão constante mudando, trabalhar com sistemas complexos requer constant experimentação e aprendizagem contínua.

Muitas vezes Sistemas Complexos estão além da capacidade humana de compreendê-los, como tudo é software nos dias de hoje. A maioria dos softwares desenvolvidos atualmente usa alguma de Iot, Big Data, AI e/ou estão integrados com inúmeros sistemas de terceiros. Esta "complexidade sistêmica" torna impossível a previsão de falhas ou mesmo entender porque os sistemas estão funcionando corretamente.

### Blameless

Se procurar um pouco na imensidão digital da internet, verá alguns relatos que Blameless faz as pessoas tornarem-se irresponsáveis porque já que elas (as pessoas) não serão culpados por um incidente, falha ou erro, elas tornam-se displicentes e sem comprometimento. Isso não é verdadeiro, as responsabilidades do papel que está exercendo numa organização devem (e continuando) as mesmas. Sobre Blameless, culpa e responsabilidade, defino +- assim:

> *"Blameless é não culpar as pessoas pelas falhas, mas sim identificar no processo as falhas e corrigi-las. Sem deixar de lados as responsabilidades inerentes da função.*"

O livro [Behind Human Error](https://www.amazon.com.br/Behind-Human-Error-David-Woods/dp/0754678342) mostra a diferença de abordagem quando o erro humano é principal responsável (primeira história) por uma falha e quando ele está inserido num contexto mais complexo (segunda história).

#### Primeira história - A visão antiga do erro humano

>- Erro humano é visto como a causa da falha
>- Dizer o que as pessoas deveriam ter feito é um forma satisfatória para descrever um fracasso
>- Dizer às pessoas para serem mais cuidadosas fará com que o problema desapareça

#### Segunda história - A nova visão do erro humano

>- Erro humano é visto como o efeito da vulnerabilidade sistêmica profunda dentro de uma organização
>- Dizer o que as pessoas deveriam ter feito não explica porque fazia sentido fazer o que faziam
>- Somente procurando constantemente suas vulnerabilidades as organizações podem melhorar a segurança

Aplicar uma nova cultura é um desafio maior que implantar uma tecnologia ou metodologia. É necessário repetir continuamente (como um  [Kata](https://en.wikipedia.org/wiki/Toyota_Kata)) que as pessoas não serão punidas ao errarem. Blameless é o pilar para implantar outras coisas que são relevantes em organizações de alta performance como: **Postmortem**, [Wheel of Misfortune](https://landing.google.com/sre/book/chapters/accelerating-sre-on-call.html#xref_training_disaster-rpg), [Game Day](https://www.slideshare.net/jesserobbins/ameday-creating-resiliency-through-destruction) e [Chaos Engineering](http://principlesofchaos.org/).   

**Referência**:

- Relatório CENIPA -  http://www2.anac.gov.br/arquivos/RF3054.pdf

- Voo JJ 3054: as lições da maior tragédia da aviação brasileira- http://www.bbc.com/portuguese/brasil-40539541

- Acidente da TAM resultou em mudanças para aumentar segurança em Congonhas - http://agenciabrasil.ebc.com.br/geral/noticia/2017-07/acidente-da-tam-resultou-em-mudancas-para-aumentar-seguranca-em-congonhas

- Was it technical failure or human error? - https://www.youtube.com/watch?v=Ygx2AI2RtkI

- Blameless Postmortem - https://codeascraft.com/2012/05/22/blameless-postmortems/

- Complex Systems - https://en.wikipedia.org/wiki/Complex_systems

- ICE (DevOps) - http://radar.oreilly.com/2015/01/devops-keeps-it-cool-with-ice.html

- Wheel of Misfortune - https://landing.google.com/sre/book/chapters/accelerating-sre-on-call.html#xref_training_disaster-rpg)

- Game Day- https://www.slideshare.net/jesserobbins/ameday-creating-resiliency-through-destruction

- Chaos Engineering - http://principlesofchaos.org/


<iframe src="//www.slideshare.net/slideshow/embed_code/key/4YtfFPiWV9Ggvy" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/fernandoike/blameless-a-culpa-nao-e-sua" title="Blameless: A culpa não é sua" target="_blank">Blameless: A culpa nao é sua</a> </strong> from <strong><a href="https://www.slideshare.net/fernandoike" target="_blank">Fernando Ike</a></strong> </div>
