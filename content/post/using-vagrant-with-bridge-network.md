+++
title = "Using vagrant with bridge network"
date = "2013-09-20"
draft = false
categories = ["SL", "english", "debian", "devops"]
tags = ["english", "SL", "vagrant", "devops"]
+++
I needed to use vagrant with bridge network in a project and the
official documentation isn’t clear about it.

Well, it’s simple, you should change the *“Vagrantfile”* in
”**config.vm.network**” parameter. E.g. using bridge on wlan0.

```
config.vm.network :public_network, :bridge => 'wlan0'
```
