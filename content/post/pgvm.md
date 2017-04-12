+++
title = "PGVM"
date = "2013-02-25"
draft = false
Categories = ["portugues", "SL", "postgresql", "pgvm"]
Tags = ["portugues", "SL", "postgresql", "pgvm"]
+++
O [PGVM](https://github.com/guedes/pgvm) é um projeto muito
interessante, inspirado no [RVM](http://www.rvm.io) (Ruby Version
Manager), ele permite gerenciar múltiplas e diferentes versões do
[PostgreSQL](http://www.postgresql.org) num mesmo computador.

Caso você esteja usando o PGVM e [Debian](http://www.debian.org) poderá
ter problema para compilar algumas versões do PostgreSQL porque estas
versões tem um pequeno bug ao executar o ”***./configure***”. Ele não
atribuem alguns parâmetros para variável do **LDFLAGS**. Se estiver
curioso para ler mais sobre, recomendo ler a discussão na lista dos
desenvolvedores do
PostgreSQL([pgdg-hackers](http://archives.postgresql.org/pgsql-hackers/2012-12/msg01058.php)).
Exemplo do erro:

```
$pgvm install 9.2.2
downloading 'http://ftp.postgresql.org/pub/source/v9.2.2/postgresql-9.2.2.tar.gz', please be patient... done.
checking 'postgresql-9.2.2.tar.gz' integrity... done.
extracting postgresql-9.2.2.tar.gz ... done.
configuring PostgreSQL Version: 9.2.2 ... done.
compiling ... ERRO: can not compile PostgreSQL 9.2.2, see make.error.log for details.
```

Se quiser ver os erros de compilação do PGVM, pode ver no arquivo
*make\_error.log

```
$less ~/.pgvm/src/postgresql-9.2.2/make.error.log
```

Para contonar este problema de compilação, basta passar os parâmetros
para variável LDFLAGS antes e usar o PGVM.

```
LDFLAGS="-Wl,--as-needed" pgvm install 9.2.2
```

Isso não é necessário para as versões mais recentes da séries 9.2, 9.1 e
9.0 (não testei em outras séries como 8.4) mas para instalar a 9.2.2,
9.1.7, 9.0.11 e (respectivamente as versões das séries) anteriores terá
que obrigatoriamente adicionar os parâmetros no LDFLAGS. ;)
