+++
title = "Octopress e post em modo rascunho"
date = "2013-05-23"
draft = false
Categories = ["portugues", "SL", "octopress"]
Tags = ["portugues", "octopress"]
+++
Quando crio um novo post, às vezes esquece de adicionar o campo
**published** configurado como false. Ele possibilita você trabalhar num
post até que ele estar finalizado sem que seja publicado, somente no
modo preview (*rake preview*)que você conseguirá ver o post inacabado e
fazer testes dele.

Depois de criar um novo post com *rake new\_post*, precisar acrescentar
um o campo published configurado como false:

```
published = false
```

Ao finalizar o post, basta troca **false** por **true**.


```
published = false
```

Também pode fazer uma modificação no Rakefile, assim ao criar um post
draft = false

```ruby
...
desc "Begin a new post in #{source_dir}/#{posts_dir}"
task :new_post, :title do |t, args|
  if args.title
    title = args.title
  else
    title = get_stdin("Enter a title for your post: ")
  end
  raise "### You haven't set anything up yet. First run `rake install` to set up an Octopress theme." unless File.directory?(source_dir)
  mkdir_p "#{source_dir}/#{posts_dir}"
  filename = "#{source_dir}/#{posts_dir}/#{Time.now.strftime('%Y-%m-%d')}-#{title.to_url}.#{new_post_ext}"
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
title = "Octopress e post em modo rascunho"
date = ""
published = false
Categories = [
```
