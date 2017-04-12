+++
title = "Git apagando um branch remoto"
date = "2012-12-12"
draft = false
Categories = ["portugues", "git", "SL"]
Tags = ["portugues", "git", "branch"]
+++
![](/images/220px-Toshiba_Remote_Control_CT-9863.jpg)

Nota rápida sobre Git e branch remoto. Estava precisando apagar um
branch que trabalhei algum (muito) tempo atrás do repositório remoto e
não estava lembrando como fazer: Bate-cabeça aqui, bate-cabeça ali e eis
que fui consultar o [manual do
Git](http://git-scm.com/book/en/Git-Branching-Remote-Branches).

    #git push origin :branch

O ”**origin**” é o apelido do repositório remoto e o ”**:branch**” é
nome do branch a ser apagado.

Simples, fácil de esquecer e difícil de achar novamente no manual. :P
