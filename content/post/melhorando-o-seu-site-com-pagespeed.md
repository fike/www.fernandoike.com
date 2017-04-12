+++
title = "Melhorando o seu site com pagespeed"
date = "2013-07-30"
draft = false
Categories = ["web performance", "debian", "SL", "portugues"]
Tags = ["portugues", "debian", "web performance", "FEO", "SL", "pagespeed"]
+++
[Front End Optimization(FEO)](http://www.yottaa.com/why-yottaa/technology/front-end-optimization/)
é um dos buzzwords mais comentados nos últimos tempos. São vários
métodos/técnicas que permite ao navegador carregar mais rapidamente as
páginas HTML.

De certa foram, FEO é uma área parecida com segurança para uma equipe de
desenvolvimento. Exige muito tempo e atenção aos detalhes mas se
incorporado, permite ganhos visíveis de audiência, conversão de vendas,
etc.

Muitos avaliam que investir em FEO é um desperdício porque o mundo (em
sua maioria) está indo em direção aos aplicativos nativos das
plataformas móveis (mobile) ao invés de concentrar todos os esforços em
aplicações base [HTML(5)](http://pt.wikipedia.org/wiki/HTML5). Fato ou
não as duas formas coexistirão mas isso fica para um próximo texto.
Voltando ao assunto título deste texto:
[Pagespeed](https://developers.google.com/speed/pagespeed/)

Ele é um serviço de otimização de sites alterando as páginas de um site
para obter a melhor performance possível usando coisas como: *CSS
sprites*, *otimização de imagens*, *defer de javascript*, *minify*, etc.
Se você não quiser usar o serviço e usá-lo diretamente no seu servidor
web pode pois o código do módulo é Código Aberto ([Apache License](http://www.apache.org/licenses/LICENSE-2.0)). A restrição é que
é que o módulo está disponível para [Nginx](http://nginx.org/) e
[Apache](http://http.apache.org/).

Os testes foram realizados usando Apache e [Debian
Wheezy](http://www.debian.org/releases/wheezy/) e meu blog com
[Octopress](http://www.octopress.org/). Na página do módulo tem os
detalhes da instalação, basicamente é baixar o pacote .deb e instalá-lo.

    #wget -c https://dl-ssl.google.com/dl/linux/direct/mod-pagespeed-stable_current_amd64.deb
    #dpkg -i mod-pagespeed-stable_current_amd64.deb

Por padrão o módulo não é ativo, pode fazê-lo diretamente no
**VirtualHost** ou a ativar para todos os existentes. Mas cuidado, não
vá alterar habilitar para todos os sites pois algumas alterações podem
quebrar o layout do site. Faça uma homologação antes. Para este teste
foi alterado o pagespeed.conf em
**/etc/apache2/mods-avaliable/pagespeed.conf** de *Off* para *On* e
depois ativado com **a2enmod**.

    #vi /etc/apache2/mods-available/pagespeed.conf


        # Turn on mod_pagespeed. To completely disable mod_pagespeed, you
        # can set this to "off".
        ModPagespeed on
    [...]

    #a2enmod pagespeed

A documentação é bem detalhada e recomendo a leitura. Se quiser ver como
um filtro é aplicado, pode ver no
[Modpagespeed](http://www.modpagespeed.com/). Os detalhes de cada uma
pode acessar
[aqui](https://developers.google.com/speed/pagespeed/module/filters).

    #vi /etc/apache2/site-avaliable/www.fernandoike.com

    [...]
            ModPagespeedEnableFilters combine_css
            ModPagespeedEnableFilters combine_javascript
            ModPagespeedEnableFilters rewrite_css,sprite_images
            ModPagespeedEnableFilters rewrite_javascript
            ModPagespeedEnableFilters inline_css
            ModPagespeedEnableFilters inline_javascript
            ModPagespeedEnableFilters rewrite_images
            ModPagespeedEnableFilters insert_img_dimensions
            ModPagespeedEnableFilters remove_comments
            ModPagespeedEnableFilters extend_cache
            ModPagespeedEnableFilters remove_quotes
            ModPagespeedEnableFilters defer_javascript
            ModPagespeedEnableFilters flatten_css_imports
            ModPagespeedEnableFilters lazyload_images
            ModPagespeedEnableFilters recompress_images
            ModPagespeedEnableFilters move_css_above_scripts
            ModPagespeedDomain http://www.fernandoike.com

    [...]

Feito as configurações, vamos aos resultados. Eles foram feito com o\
 [Webpagetest (WPT)](http://www.webpagetest.org/) e todos baseados no
Firefox e uma conexão de *5 Mbit/s*.

Teste feito em Virgínia nos EUA sem PageSpeed.

![](/images/dulles_s_pagespeed2.png)

O Document Complete (tempo que o navegador levou para deixar a página
“pronta” para usar) ou Onload foi entregue me *3,972 segundos*, *56
requisições* e *1.535 Kbytes* de tamanho. Um bom resultado para um blog.

Teste feito em Virgínia nos EUA com PageSpeed.

![](/images/dulles_c_pagespeed2.png)

Teste feito em São Paulo sem PageSpeed.

![](/images/sp_s_pagespeed2.png)

Teste feito em São Paulo com PageSpeed.

![](/images/sp_c_pagespeed2.png)

Tabulando para facilitar a comparação:

EUA
---

  Virginia |s/ PageSpeed | c/ PageSpeed
  ------------ | -------------- | --------------
  Doc Complete | 3,972 seg.  |   2,451 seg.
  Requisicoes | 56 |            39
  Tamanho     |  1.535 Kbytes | 646 Kbytes

Brasil
------

  São Paulo | s/ PageSpeed | c/ PageSpeed
  ------------ | ------------ | --------------
  Doc Complete | 6,360 seg.  |   4,696 seg.
  Requisicoes | 51 |   40
  Tamanho | 1.535 Kbytes | 941 Kbytes



O resultado com PageSpeed em Virgínia teve uma redução drástica no
tamanho da página, em torno de *42%*, *39%* no Doc Complete e *30%* em
requisições.

Agora em São Paulo as reduções foram: 39% no tamanho da página, *26%* no
Doc Complete e *22%* de requisições.

Fazendo configurações básicas dos filtros do PageSpeed consegue uma boa
otimização. Considerando o baixo esforço para implementá-lo, é altamente
recomendável mas é importante homologar as alterações feitas por ele
porque\
 pode quebrar o layout das páginas.

A distância geográfica impacta na experiência do usuário, como o
servidor do teste está em Dallas e Virgínia é mais perto que São Paulo,
é perceptível o impacto no tempo do Doc Complete ao comparar as duas
localidades. Existem maneiras de melhorar o resultado de São Paulo se
usar uma CDN mas isso fica para outro texto.
