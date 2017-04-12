+++
title = "Instalando o veewee"
date = "2014-06-05"
draft = false
Categories = ["SL", "debian", "portugues"]
Tags = ["portugues", "debian", "veewee", "nokogiri", "kvm", "vagrant"]
+++
[Veewee][veewee] é uma ferramenta para criar templates para o
[Vagrant][vagrant], [KVMs][kvm] e outros sistemas de virtualização. Costumo usá-lo para
criar imagens com alguns serviços instalados para desenvolver algum sistema
ou testar alguma solução/prova de conceito.

Se for instalar o veewee usando Ruby gerenciado pelo rvm, depois da instalação será necessário alterar a versão do ruby no arquivo **rvmrc**. No momento que foi escrito este   texto a versão estável do [Ruby][ruby] é 2.1.2.

Baixando o Veewee
```
$git clone https://github.com/jedi4ever/veewee.git veewee
```

Instalando...
```
fike@klatoon:~/d/veewee$ bundle install
```

Uma das despendências do Veewee é o [Nokogiri][nokogiri] e ele depende da libxml2. Se
quiser usar o Nokogiri com a libxml2 empacotado para seu linux terá que
reinstalar ele.

```
$gem install nokogiri -- --use-system-libraries
```

Para este post, o box que será criado é o [Debian][debian] Wheezy 7.5 32 bits
(i386). Outras distribuições Linux ou outros sistemas operacionais com templates
disponíveis.
```
$veewee vbox templates
```

Criando as definições para criar o box para o Vagrant.

```
$veewee vbox define 'debtest' 'Debian-7.5.0-i386-netboot'
```

No diretório definitions estão scripts de instalação e personalizações. Se
precisar de algum modificação da instalação, é aí que deve alterar. Por exemplo,
trocar o idioma padrão que será instalado.

```
sed -i 's/en\_US/pt\_BR/g' definitions/debtest/preseed.cfg
```

Muitas outras modificações podem ser feitas, veja a documentação e veja os scripts que
estão nas definições do template.

Criando o vm.
```
$veewee vbox build 'debtest'
```

Se precisar instalar ou configurar alguma outra que não foi abordado pelos
scripts que no diretório definitions, pode entrar via ssh.
```
ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -p 7222 -l vagrant 127.0.0.1
```

Para verificarse a box está ok.
```
$veewee vbox validate 'debtest
```

Exportar a box.
```
$veewee vbox export 'debtest'
```

Com a box pronta é só importar para o Vagrant.
```
$vagrant init 'debtest'

$vagrant box add 'debtest' '/home/fike/d/veewee/debtest.box'
```

[veewee]:  https://github.com/jedi4ever/veewee
[vagrant]: http://www.vagrantup.com/
[kvm]: http://www.linux-kvm.org
[ruby]: https://www.ruby-lang.org/
[nokogiri]: http://nokogiri.org/
[debian]: http://www.debian.org/
