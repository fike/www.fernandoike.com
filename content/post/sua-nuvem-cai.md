+++
title = "Sua nuvem cai"
date = "2013-12-18"
draft = false
Categories = ["devops", "portugues"]
Tags = ["portugues", "devops", "portugues", "sysadmin"]
+++
Você acha que Cloud Computing são nuvens bonitinhas como essas?

![]( /images/clouds-33.jpg)

Ou ela está mais para isso?

![]( /images/thunderstorm-is-coming.jpg)

Existe um falso mito que hospedar os servidores ou aplicação na nuvem
(ou cloud se preferir…). Não é mais necessário se preocupar com
problemas de disponibilidade como: geradores de energia elétrica, banco
de baterias (nobreak), circuitos redundantes de rede lógica e elétrica,
segurança patrimonial, etc. Entretanto ao usar algum serviço de nuvem,
você está delegando essas preocupações para outra empresa.

Nesse mês (Dezembro de 2013) muitas empresas que hospedam suas
aplicações na nuvem foram surpreendidas porque um datacenter teve uma
indisponibilidade do tipo citada acima. O datacenter, bem conhecido,
teve um problema de energia elétrica e praticamente tornou indisponível
todos os sistemas que estão ali hospedados, dentre eles alguns dos
principais fornecedores de cloud e consequentemente todos os clientes
deles também tiveram seus sistemas indisponíveis.

Um problema deste tipo num datacenter é difícil de acontecer mas
acontece, aconteceu e acontecerá. É como um acidente de avião, são
várias pequenas coisas que aparentemente não poderiam derrubar uma avião
mas elas encadeadas derrubam. No caso de um datacenter são um conjunto
de pequenos incidentes/problemas que podem torná-lo indisponível.

O falso mito que ao colocar uma aplicação/sistema na nuvem, ele nunca
ficará indisponível porque na nuvem as coisas funcionam automagicamente
é mais comum que possa imaginar. Pense um pouco, todo sistema precisa
estar armazenado em algum lugar, se não está na empresa precisa estar em
outro lugar mesmo na nuvem. A nuvem([IaaS](http://en.wikipedia.org/wiki/Infrastructure_as_a_service#Infrastructure_as_a_service_.28IaaS.29),
[SaaS](http://en.wikipedia.org/wiki/Software_as_a_service),
[PaaS](http://en.wikipedia.org/wiki/Platform_as_a_service), etc)
facilita muito porque muito coisa é entregue praticamente pronta e com
um pouco de ajuste já é possível disponibilizar um serviço rapidamente.
Entretanto mesmo na nuvem, um sistema estará alocada num ou mais
datacenters. Portanto ao considerar hospedar seu sistema numa
infraestrutura na nuvem, considere pensar no contingenciamento dele.

Veja alguns exemplos de incidentes de indisponibilidades:

-   [Furacão Irene derrubou o AWS](http://www.geekwire.com/2011/amazon-web-services-bracing-hurricane-irene-virgina/)
    (**Amazon Web Service**) (dentre os afetados estão
    [Reddit](http://www.reddit.com/) e
    [FourSquare](https://pt.foursquare.com/) em Agosto de 2011.

-   [Furacão Sandy derrubou vários datacenters](http://www.zdnet.com/hurricane-sandy-knocks-out-nyc-data-centers-websites-services-down-7000006588/)
    (dentre os sites afetados estão [Gizmodo](http://gizmodo.com) e
    [Huffington Post](http://www.huffingtonpost.com/)) em Nova York em
    Outubro de 2012.

-   Problema de energia elétrica derrubou datacenter em São Paulo e
    derrubou a AWS ([Região SA-EAST-1](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html))
    em Dezembro de 2013.

Geralmente ao colocar um sistema ou site num fornecedor de nuvem como
AWS, a maioria esquece de considerar o contigenciamento no custo
operacional. A necessidade somente é percebida posteriormente após uma
indisponibilidade como as citadas acima. Uma grande vantagem da nuvem é
permitir ter um plano de contingência mantendo quase todos serviços de
contingência desligado, mantendo somente o necessário para fazer a
sincronização dos dados de um infraestrutura para outra (de uma região
para outra no caso do AWS).

Alguns sites adotam como parte secundário do plano de contingência ter
as partes principais em cache numa [CDN (Content Delivery Network)](http://en.wikipedia.org/wiki/Content_delivery_network), tendo
como o ponto principal da contingência a redundância dos serviços numa
região geograficamente distante. Exemplo: Numa região diferente do AWS
ou num datacenter numa região diferente no caso da
[Rackspace](http://www.rackspace.com).

O caso do [Netflix](http://techblog.netflix.com/2012/10/post-mortem-of-october-222012-aws.html)
é bem interessante como estudo de alta disponibilidade e contingência
usando AWS, leitura recomendadíssima.

Se você estiver considerando migrar suas aplicações para a nuvem,
considere um plano de contingência. Se puder, construa a arquitetura de
seu site, sistema, aplicação, etc. considerando tecnologias que permitam
trabalhar de forma distribuída e com redundância. Afinal, uma empresa
com o seu negócio parado pode ser muito custoso do que alocar mais
recursos computacionais para melhorar o SLA da sistema que suporta o
negócio.

Imagens de *Charles Rondeau* e *MALIZ ONG*, elas podem ser encontradas
em [Public Domain Pictures](http://www.publicdomainpictures.net).
