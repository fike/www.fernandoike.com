+++
title = "Otimizacao de imagens no blog"
date = "2013-02-23"
draft = false
categories = ["web performance", "octopress", "portugues", "SL"]
tags = ["blog", "web performance", "octopress", "portugues", "SL"]
+++
Continuando a série sobre optimização de sites…

Meu blog foi migrado para [Octopress](http://www.octopress.org), um
pouco da saga pode ser lida aqui, e na migração houve uma melhora
significativa de performance. Porém isso pode ser perdido por uma
distração de usar imagens com tamanho (em bytes) relativamente grande.

No teste com [Webpagetest](http://www.webpagetest.org), meu site estava
levando mais de 10 segundos para ser aberto por usuário e o tamanho da
página principal passava de 1 Megabyte.

![](/images/test_img_nota_old.png)

![](/images/test_img_tempo.old.png)

Pensando em como melhorar o resultado e uma pesquisa no pai dos burros
(Google) do século 21, achei do programas que ajudam a otimizar as
imagens: [pngcrush](http://pmt.sourceforge.net/pngcrush/) e o famoso
[imagemagick](http://www.imagemagick.org/).

Alguns testes usando ambos para otimizar as imagens sem perder muita
qualidade. Para otimizar imagens com formato png, usa o pngcrush com os
parâmetros abaixo:

    $pngcrush -rem alla -brute -reduce imagem.png resultado.png

Para arquivos de imagem JPEG, pode utilizar as opções que estão listadas
abaixo:

    convert -strip -interlace Plane imagem.jpg resultado.jpg

Para não ter que fazer arquivo por aquivo a otimização das imagens, fiz
um script bem simples que executo sempre antes de criar um post novo.

Depois de executar o script e fazer o deploy das novas images, já é
perceptível a melhora de peformance, veja as notas do Webpagetest e
performance:

![](/images/test_img_nota_new.png)

![](/images/test_img_tempo_new.png)

O tamanho total da página principal do blog diminui por volta de 50% e o
tempo de resposta do blog também diminuiu perto dos 40%. Uma
significativa diferença se considerar somente a otimização das imagens
mas o mais importante é a melhora do tempo de resposta para o
internauta. :)

Obs.: Antes que esqueça, este tipo de técnica está sendo considerada
FEO. Um pouco de cuidado com mais este buzzword, não se empolgue demais.
;)
