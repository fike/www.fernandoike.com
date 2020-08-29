+++
title = "Instalando loic no debian"
date = "2013-07-12"
draft = false
categories = ["debian", "SL", "portugues"]
tags = ["debian", "SL", "portugues", "loic"]
+++
Nos últimos meses tem ocorrido muitas solicitações de clientes para
fazer testes de carga ou segurança usando LOIC. [LOIC (Low Orbit Ion
Cannon)](https://en.wikipedia.org/wiki/Low_Orbit_Ion_Cannon) é um
software desenvolvido em
[C\#](https://msdn.microsoft.com/en-us/vstudio/hh341490.aspx) e ele tem o
objetivo de fazer ataques de negação de serviço
([Denial-of-Service](https://en.wikipedia.org/wiki/Denial-of-service_attack))
ou ataques de negação de serviço dstribuído ([Distributed
Denial-of-Service](https://en.wikipedia.org/wiki/Denial-of-service_attack)).

O LOIC possibilita ataques usando
[TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol),
[UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol) ou
[HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol), ele
ou alguns derivados dele (como [JS LOIC](https://cisko.fr/)) são muito
usados pela anonymous como represália ou protesto contra algum site de
empresa, governo ou instituição política.

Bom, o LOIC para meu trabalho nesses clientes tem a função de avaliar a
capacidade de contenção/mitigação de ataques de DOS/DDOS. Geralmente
avalia-se se o
[Firewall](https://en.wikipedia.org/wiki/Firewall_(computing)), [IPS
(Intrusion Prevention
System)](https://en.wikipedia.org/wiki/Intrusion_prevention_system), [WAF
(Web Application
Firewall)](https://www.owasp.org/index.php/Web_Application_Firewall),
etc. conseguem conter esse tipo de ataque. Caso seja identificado que
não, é entregue um relatório com propostas de mudança na infraestrutura
do cliente.

Ops… Voltando ao assunto título deste artigo, a instalação no
[Linux](https://www.linuxfoundation.org/) é possível de duas maneiras:
instalando [WINE](https://www.winehq.org/)e ou instalando o
[MONO](https://www.mono-project.com/Main_Page). No meu caso instalei o
MONO e minha distribuição é o [Debian](https://www.debian.org).

O procedimento é relativamente simples:

    #aptitude install mono-complete

Para baixar o LOIC pode fazer acessando a página do projeto no
[Sourceforge](https://sourceforge.net/projects/loic/)

Após baixar, descompacte e execute o LOIC usando o MONO.

    $unzip LOIC-1.0.7.42-binary.zip
    $mono LOIC.exe

Como você pode ler, a instalação é simples. O LOIC também não é complexo
como pode ver no screenshot do Debian instalado no meu computador.

![](/images/loic.png)
