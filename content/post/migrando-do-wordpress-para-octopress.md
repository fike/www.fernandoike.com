+++
title = "Migrando do wordpress para octopress"
date = "2013-02-17"
draft = false
Categories = ["portugues", "octopress", "web performance", "SL"]
Tags = ["portugues", "octopress"]
+++
Continuando a comentar um pouco mais sobre a mudança do blog que
anteriormente era [Wordpress](http://www.wordpress.org) e agora é
[Octopress](http://www.octopress.org). Vou mostrar alguns dados
interessantes numa comparação simples e sem critério científico.

Para fazer o teste, usei o [Webpagetest](http://www.webpagetest.org/)
que tem muitas cidades no mundo para fazer o teste de performance na
perspectiva do internauta. Ele é muito interessante para testar em
diferentes países, mas para este teste usei apenas a instância do Brasil
dele que está em [São
Paulo](http://pt.wikipedia.org/wiki/S%C3%A3o_Paulo_(cidade)).

### Wordpress

![](/images/wpt_wp_notes.png)

Para um blog que está em hospedado em Dallas e tem seu maior público na
região sudeste do Brasil até que o tempo para um internauta ver o site
não está mal. Está ali na casa dos **6 segundos** para um total de **37
requisições** e considerando que o servidor não tem nenhum tipo de
ajuste de performance em qualquer parte
([kernel](http://www.kernel.org), [apache](http://httpd.apache.org),
[MySQL](http://www.mysql.org), etc.).

A única nota sofrível é o FBT (First Byte Time), isso é porque não fiz
nenhum ajuste de performance (tuning) no **Apache**, **PHP** ou
**MySQL**.

No próximo quadro você verá outras informações como tempo de
renderização, total de bytes, etc.

![](/images/wpt_wp_sum.png)

### Octopress

Meu blog perdeu algumas funcionalidades ao migrar para o **Octopress**
mas nada muito significativo que impacte fortemente na audiência ou uso
básico para postar.

Destacando que o **Octopress** é baseado no
[Jekyll](https://github.com/mojombo/jekyll) que possua vez, gera
conteúdo estático (html simples), ou seja, não precisar de nenhuma
linguagem de programação embutida no servidor.

É muito provável que esse seja a grande diferença com o **Wordpress** do
ponto de vista de peformance.

![](/images/wpt_octo_notes.png)

O tempo do site caiu para 4 segundo os e número de requisições diminuiu.
Se fosse um site com mais imagens, provavelmente a diferença de
performance seria muito maior. Veja que melhorou as notas do
[PageSpeed](https://developers.google.com/speed/pagespeed/). Aos menos
não tenhum nota em vermelho.

Ah, comentei que diminuiu mas vai aí a imagem com mais informações:

![](/images/wpt_octo_sum.png)

Se eu mantiver o pique, vou fazer mais algumas comparações. Um conclusão
que posso arriscar dizer neste pouco tempo usando **Octopress** é que se
você tem um pouco mais de conhecimento de TI e posta com frequência
relativamente exparsar , você tem uma excelenta ferramentta pra
**blogar**

Um pequeno sumário com os dados dos dois motores de blogs.

  blog           |  requisições   |  tempo
:-------------: | :-------------: | --------:
  wordpress   |       37          |   6,437s
  octpress      |      32          |  4,371s

Se gostou ou não ou mesmo tem outras considerações, comente aí embaixo.
;)
