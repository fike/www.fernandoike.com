+++
title = "Postgresql tuning"
date = "2013-08-06"
draft = false
Categories = ["performance", "postgresql", "SL", "portugues"]
Tags = ["performance", "tuning", "postgresql", "SL", "portugues"]
+++
Normalmente ao pensar em melhorar a performance do banco de dados,
muitos esquecem de modificar alguns parâmetros e configurações do
Sistema Operacional e outras coisas relacionadas a infraestrutura de TI.
Não dar a atenção devida para essas coisas é que elas podem impactar o
desempenho do banco de dados e você estar tão focado em melhorar o banco
de dados que não considera-os como a causa raiz.

Bom, então a idéia aqui é ser uma etapa prévia antes de mexer nas
configurações do [PostgreSQL](http://www.postgresql.org/), portanto
considere como um ponto de partida. Cada aplicação e arquitetura terá
uma configuração específica do PostgreSQL para que tenho o melhor
desempenho possível.

### Adote um método para fazer os ajustes de performance.

Infelizmente não existes muitos números mágicos (ok, existe alguns
números mágicos mas não é caso neste momento). Para fazer os ajustes
para melhorar o desempenho do PostgreSQL e consequetemente da aplicação
é necessário fazer vários testes em muitas variáveis. Fazer alterações
em muitas variáveis ao mesmo tempo pode levar muito mais tempo do que
fazer alterações em poucas ou uma variável e observar se obteve ganho de
performance ou não. Portanto, adote uma metodologia, faça uma mudança
por vez e teste! Anote os resultados, faça outra alteração e compare
coms os resultados anteriores. Assim poderá comparar e verificar quais
são os melhores ajustes em determinados cenários que imaginar que a
aplicação faz.

Vale qualquer forma de registro, até papel de padaria!

### Armazenamento

Tão ou mais importante que ter uma servidor com uma capacidade tão
grande de processamento é ter a parte de armazenamento (discos/storages)
bem plenajada. É muito comum usar Storages com um único Array e
compartilho entre as diversas aplicacṍes da instituição.

Como aparentemente o Storage tem I/O infinito, geralmente é relegado
algum planejamento de como as aplicações ou base de dados irão ocupá-lo.
Em situações de grande uso de I/O (escrita ou leitura) é importante
criar grupos de discos (arrays) considerando usar as partes mais rápidas
do Storage para as bases ou operações críticas e com conexões de fibras
dedicadas para o servidor PostgreSQL.

O Telles escreveu um [bom
texto](http://savepoint.blog.br/postgresql-discos-cia/) sobre discos,
recomendada a leitura.

Considere sempre usar “canais” dedicados de comunicação entre o servidor
do banco de dados e o armazenamento. Exemplo: Caso esteja usando um
sistema de arquivo de rede
([NAS](http://pt.wikipedia.org/wiki/Network-Attached_Storage)) para o
banco de dados, considere segregar em uma rede dedicada à eles para que
não haja concorrência de tráfego de rede com outros serviços e/ou
aplicações. Caso esteja usando comunicação via Fiber Channel
([SAN](http://pt.wikipedia.org/wiki/Rede_de_%C3%A1rea_de_armazenamento)),
tente deixar as conexões físicas dedicadas entre o servidor de banco de
dados, switch fiber channel e o storage.

Armazenamento de banco de dados é um tema tão vasto que facilmente
poderia ser um Livro de centenas de páginas mas por enquanto ficamos por
aqui…

### Habilitar ou não o HyperThreading

Para o PostgreSQL não faz diferença se o
[HyperThreading](http://pt.wikipedia.org/wiki/Hyper-threading)
habilitado ou não, ele usará o número máximo de processadores que o
Sistema Operacional disponibilizar.

### Sistema Operacional

É simples, use Unix/Linux e que seja 64 bits. Entendo que exista
questões de usar um Sistema Operacional “homologado” para o servidor ou
Storage mas se quer o máximo de performance seria melhor usar
[CentOS](http://www.centos.org/) ou [Debian[7](http://www.debian.org/)
ou mesmo um [ArchLinux](https://www.archlinux.org/).

Antes do tuning do banco de dados, tuning do Sistema Operacional.

Isso é coisa básica mas extremamente importante, afinal é impossível
aumentar o*Shared Buffer* do PostgreSQL sem aumentar a memória
compartilhada do Linux. Considere aumentar a memória compartilhada
(*Shared Memory*), *semáforos*, buffers de rede, scheduler I/O, etc.

#### Memória compartilhada (shared memory)

Mais ou menos 25% da memória total é a resposta padrão mas pode ser
interessante iniciar os ajustes com valor menor. Algo entre 15% e 20% do
total disponível da RAM e depois ajustar para um valor maior. Exemplo
para 10GB:

    #sysctl -w kernel.shmmax=109951162777

*Observação do Euler*: À partir da versão 9.3 do PostgreSQL, [não será
mais
necessário](http://wiki.postgresql.org/wiki/What's_new_in_PostgreSQL_9.3#Switch_to_Posix_shared_memory_and_mmap.28.29)
configurar a memória compartilhada para o PostgreSQL.

#### Usando Swap somente em último caso

O Kernel Linux por padrão usa a memória
[Swap](http://pt.wikipedia.org/wiki/Mem%C3%B3ria_virtual) (“extensão” da
memória RAM na HD, é muito) antes mesmo de esgotar o espaço livre da
memória RAM. Para utilizar a Swap somente em último caso:

    #sysctl -w vm.swappiness=0

Também pode fazer uma [outraabordagem](http://www.postgresql.org/docs/9.2/static/kernel-resources.html)
    do uso do Swap alterando o **vm.overcommit**.

    sysctl -w vm.overcommit_memory=2

### Rede

Supondo que o servidor tem placas de rede de 10GBits/s.


    #systcl -w net.core.rmem_default = 8388608
    #systcl -w net.core.rmem_max = 8388608
    #systcl -w net.core.wmem_default = 8388608
    #systcl -w net.core.wmem_max = 8388608
    #systcl -w net.core.netdev_max_backlog = 10000

#### Ajustes na pilha de rede.

    #systcl -w net.ipv4.tcp_max_syn_backlog = 40000
    #systcl -w net.core.somaxconn=4000
    #systcl -w net.ipv4.tcp_timestamps = 0
    #systcl -w net.ipv4.tcp_sack = 1
    #systcl -w net.ipv4.tcp_window_scaling = 1
    #systcl -w net.ipv4.tcp_fin_timeout = 15
    #systcl -w net.ipv4.tcp_keepalive_intvl = 30
    #systcl -w net.ipv4.tcp_tw_reuse = 1

### Scheduler I/O

O Kernel Linux tem vários tipos de scheduler, por padrão atualmente é o
[CFQ](http://en.wikipedia.org/wiki/CFQ) mas para operações intensivas de
I/O o [Deadline](http://en.wikipedia.org/wiki/Deadline_scheduler) tem um
resultado melhor.

*Observação*: Euler, o Grande pai mestre de PostgreSQL no Brasil
comentou comigo que em alguns cenários é melhor usar CFQ.

    #echo deadline > /sys/block/sda/queue/scheduler

### Limite de Arquivos Abertos (Open Files Limit)

Acontece com muita frequencia alterar a configuração do Linux, servidor
de aplicação, algoritimos, banco de dados e esquecer de alterar o
“Limite de Arquivos Abertos”. Não alterá-lo significa numa analogia
grosseira dizer que “você está andando de Porche com o freio de mão
puxado.”. Este item é importantíssimo porque se estiver com valores
relativamente baixos, nenhuma ferramenta de monitoramento irá detectar
isso como um gargalo de desempenho.

## com um limite maior:

Edite o */etc/pam.d/common-session*, acrescente, salve e feche o
arquivo.

    session    required   pam_limits.so

Edite o */etc/security/limits.conf* e acrescente as linhas abaixo:

     *               soft     nofile          65536
     *               hard     nofile          65536

Lembre-se de salvar, fechar o arquivo e reinicar para que as alterações
tenham efeito. Para saber mais, vale ler a
[documentação](http://docs.basho.com/riak/latest/ops/tuning/open-files-limit/)
do Riak sobre isso.

*Observação do [Euler](http://eulerto.blogspot.com.br/)*: O valor 65536
pode ser um pouco exagerado, exceto em bases muio grandes.

### Sistema de Arquivo

Esse é um difícil dizer qual é a melhor opção, eu não conheço benchmarks
recentes mas o benchmark que fiz algum tempo atrás apontou que para
bases de dados pequenas e de pouco usuários simultâneos é melhor usar
[Ext4](http://pt.wikipedia.org/wiki/Ext4). No cenário de base de dados
grandes e muitos usuários simultâneos o
[XFS](http://pt.wikipedia.org/wiki/XFS) tem uma performance melhor.

Também é imporante fazer outros ajustes como modificar a montagem dos
discos para desconsiderar o timestamp da criação/edição de arquivos e
diretórios. Exemplo de entrada no */etc/fstab*:

    [...]
    /dev/sdd1   /opt/pg/9.3/db   xfs defaults,noatime,nodiratime,nodev  0 0
    [...]

Se você tiver alguma informação do
[Brtfs](https://btrfs.wiki.kernel.org/index.php/Main_Page), Ext4 e XFS
com benchamrks mais novos, comente aí. :D

### Conclusão

Pensar em tuning de banco de dados sem considerar os ajustes de
desempenho de toda arquitetura envolvida é como colocar um motor de
Porsche num Fusca. Tuning é uma tarefa contínua enquanto a aplicação
existir. Existe bons textos sobre o tema, recomendo a leitura de alguns:

-   [Red book Linux Performance and Tuning
    Guidelines](http://www.redbooks.ibm.com/abstracts/redp4285.html)

Livro antigo mas com informações preciosas.

-   [Linux Performance Tuning - Riak -
    Basho](http://docs.basho.com/riak/latest/cookbooks/Linux-Performance-Tuning/)

Bem didádico, as dicas estão aplicadas para o Riak mas vale como
referência.

-   [Linux Performance Guide -
    Neo4J](http://docs.neo4j.org/chunked/stable/linux-performance-guide.html)

Também bem didático mas aplicado para o Neo4J.

Neste texto tem uma visão bem particular, se tiver alguma sugestão,
crítica ou correção. Faça! :)
