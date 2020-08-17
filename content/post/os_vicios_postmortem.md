+++
title = "Os vícios ao escrever um Postmortem em Falhas de Sistemas Complexos"
date = 2020-08-17T15:29:12-03:00
draft = false
description = "Algumas reflexões sobre os vícios ao escrever Postmortem"
categories = ["postmortem", "devops", "sre", "portugues"]
tags = ["postmortem", "devops", "sre", "portugues"]
+++
![](/images/pencil-918449_640.jpg)

Postmortem em tecnologia é relatado bem antes do Google lançar o livro sobre SRE (2016), 4 anos antes John Allspaw escreveu também a respeito no texto "[Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)".

A maioria das referências sobre como escrever relatórios de Postmortem seguem mais ou menos essa estrutura de relatório do livro do Google. Algumas outras abordagens de como escrever e conceitos aplicados foram abordadas por mim no texto "[Blameless Postmortem](https://www.fernandoike.com/2017/09/07/blameless-postmortem/)".

Escrever Postmortem tem se tornado parte da cultura na área de Tecnologia da Informação desde o texto de John Allspaw, com o crescimento também tem se tornado comum alguns vícios que podem influenciar negativamente a aprendizagem envolvida neste processo.

# Escrever Postmortem não é para ser sacrifício

Quando uma equipe começa a escrever um Postmortem é comum algumas pessoas da equipe ou de outras acharem um desperdício de tempo coletando evidências, conversando com as pessoas e analisando os processos envolvidos para identificar a cadeia de eventos que gerou um incidente.

Este não é um feedback loop tradicional realizado com frequência, ele só ocorre quando acontece incidente. É difícil no começo escrever postmortem sem um viés e já apontar para pessoas ou para efeitos e não as causas de incidente.

A lista de atividades a serem executadas devem entrar no ciclo usual das equipes com a devida severidade, ou seja, priorizada conforme a criticidade do incidente e o impacto da atividade para que não ocorra. É comum que as pessoas que estão nos papéis como Product Owner, Product Manager, Analista de Negócio não serem envolvidas no Postmortem, Elas devem participar para ajudarem mensurar em conjunto com as pessoas que estão nos papéis técnicos (desenvolvedores, operações de TI, segurança, qualidade, etc.) os impactos do ponto de vista de produto ou negócio.

A participação pode ser total ou parcial dependendo de como sãos os fluxos de trabalho, isso ajuda diminuir a fricção sobre o que priorizar no backlog porque todos os principais papéis sabem se é realmente importante ou não priorizar.

A mudança de um estado de sacrifício para algo importante de aprendizagem, conhecimento e crescimento pode ocorrer depois de algum tempo escrevendo postmortem, priorizando o backlog e os mesmos tipo de incidentes não ocorrendo novamente.

Cito como um caso de um das startups que trabalhei e ajudei implementar o Postmortem alguns anos atrás. Nas primeiras vezes a participação era praticamente inócua, após alguns relatórios com resoluções práticas de mudança em sistemas, processo ou acesso, se tornou corriqueiro e parte da equipe tomou para si a responsabilidade de escrever sem a necessidade de lembrá-los.

# Os 5 Porquês (Whys)

Os 5 porquês é muito usado para ajudar encontrar a causa raiz de um incidente, ele é bem interessante como auxílio ao entender a cadeia de eventos que geraram um incidente. Um exemplo prático está logo abaixo, um incidente envolvendo a indisponibilidade de um site.

1- Por que o site caiu?

2- Por que o banco de dados está aceitando mais conexões?

3- Por que o banco de dados atingiu o limite de conexões?

4- Por que as transações no banco de dados não estão sendo finalizadas?

5- Por que o banco de dados está sem um índice para essas consultas?

No quinto por que foi encontrado o que deveria ser a causa-raiz. A equipe identificou que a causa-raiz era falta de índice no banco de dados. No entanto, ao fazer as mesmas perguntas com uma equipe diferente da primeira ou iterar mais um pouco com mais perguntas a causa-raiz pode ser um pouco diferente.

1- Por que o site está indisponível?

2- Por que o banco de dados não aceita mais conexões?

3- Por que havia conexões da aplicação presa no banco de dados?

4- Por que as transações estavam muito lentas?

5- Por que foi esquecido de adicionar o índice do campo novo?

6- Por que não foi criado o teste para identificar a falta do índice

Se executar o 5 Whys uma terceira vez juntando as duas equipes, a sequência teria diferença.

Isso acontece porque esta técnica é subjetiva, não tem nada de errado em usá-la para levantar as primeiras hipóteses sobre a cadeia de eventos de um incidente. Ela é muito útil quando uma equipe ainda está aprendendo a escrever um Postmortem a utilizarem a dedução para entender a cadeia de eventos.

Há diversas críticas sobre 5 Whys, o Banco de Desenvolvimento da Ásia compilou algumas delas (tradução livre):

>1 - A tendência da investigação parar nos sintomas e não continuar investigando mais profundamente até encontrar as causas-raiz.
>
>2 - A falta de habilidade de quem está investigando além dos atuais conhecimentos.
>
>3 - Dificuldade em apoiar e facilitar quem está investigando a fazer as perguntas certas.
>
>4 - Dificuldade de reproduzir os resultados: equipes diferentes usando a técnica do 5 Whys chegam em causa diferentes ao mesmo problema.

# O viés da causa raiz

O senso comum é de que causa-raiz é a identificação de qual evento foi que iniciou um incidente. Contudo, se o evento que gerou o incidente não for a causa-raiz, qual foi?
Não aprofundar, quando necessário, a análise para identificar quais forams as causas de um incidente, pode levar a ações pouco efetivas para que o mesmo problema não ocorra novamente. É comum nos primeiros relatórios Postmortem não ser considerado as ações das pessoas, as suposições que elas tinham ao tomarem as ações durante um incidente. O primeiro caso do 5 Whys neste texto é um exemplo de conclusão que não considera os fatores humanos, mesmo não aplicando o 5 Whys.

O segundo caso citado no 5 Whys aprofunda um pouco mais, mas será que ele realmente chegou na causa raiz?

* Uma das possibilidades factíveis é que realmente foi por esquecimento a não criação de índice e o respectivo teste. Uma outra possibilidade é porque as pessoas da equipe podem não saber este tipo de teste ou mesmo não sabem fazer nenhum tipo de teste.
*  Definido uma nova função de compra
* Criado a instrução para adicionar a coluna sem índice
* Os testes unitários não tinham cobertura para este problema
* Revisores do Pull Request/Merge Request não viram a falta de índice
* A coluna sem índice não degradou o desempenho nos testes de carga
* A função foi implementada em produção sem degradar desempenho
* Após campanha de marketing da nova função, as compras usando a nova função aumentaram para 30% do total e o site caiu.

Uma sequência dedutiva para cadeia de eventos deste incidente seria:

* Definido uma nova função de compra
* Criado a instrução para adicionar a coluna sem índice
* Os testes unitários não tinham cobertura para este problema
* Revisores do Pull Request/Merge Request não viram a falta de índice
* A coluna sem índice não degradou o desempenho nos testes de carga
* A função foi implementada em produção sem degradar desempenho
* Após campanha de marketing da nova função, as compras usando a nova função aumentaram para 30% do total e o site caiu.

Os eventos isolados sozinhos não seria suficiente para o incidente acontecer, mas a sequência de encadeada de ações e eventos gerou o incidente. Qual seria a causa-raiz no exemplo acima? O índice faltando no campo?

A resposta rápida é sim, mas a uma resposta uma pouco mais longa é de que o incidente poderia ser evitado em várias partes do processo. Na revisão mais extensa do código, criação de um teste de carga para nova função de compra, um teste unitário ou de integração específico, etc.

Algumas dessas ações não são rápidas para finalizar e manter o site funcionando, uma solução de contorno poderia limitar a quantidade de compras pela nova função para 1.000 transações por segundo (ressaltando que é um exemplo hipotético). A análise até o momento destacou apenas a parte técnica mas cabe olhar numa outra perspectiva:

* A equipe responsável pela função tinha as habilidades para evitar que o incidente acontecesse?
* Se eles tivessem a documentação ou referências do que era a funcionalidade evitaria? Se eles soubessem técnicas como Test-Driven Development evitaria o incidente?
* A equipe estava trabalhando no limite da capacidade?

Um bom relatório Postmortem, por exemplo, teria algumas dessas perguntas analisadas, identificado se a falta de índice foi porque a equipe estava sobrecarregada ou esquecendo de adicionar o índice. Ressaltando, poderia ser outras questões levantadas relacionadas as pessoas ou mesmo processos.

Quase nunca um incidente é gerado por causa de um único evento, quase sempre está relacionado há uma sequência de eventos envolvendo as interações pessoas, processos e software. É um sistema complexo, falhas acontecem o tempo todo e abraçar a complexidade observando o que induziu o erro humano é quando realmente o processo de Postmortem se torna parte do processo de aprendizagem de toda organização.

Por fim, é fundamental abraçar a complexidade e as falhas se as organizações querem aprender mais rapidamente.

E você, já colocou em prática no dia a dia ou ainda tem alguma dúvida sobre o assunto? Conta pra gente nos comentários!

**Referências**:

* [5 Whys and Other Lies About Complex System Failures — Jessica DeVita](https://youtu.be/fCVLdn2Ncf4)
* [5 Whys Technique](https://www.adb.org/sites/default/files/publication/27641/five-whys-technique.pdf)
* [Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems)
* [Blameless Postmortem](https://www.fernandoike.com/2017/09/07/blameless-postmortem/)