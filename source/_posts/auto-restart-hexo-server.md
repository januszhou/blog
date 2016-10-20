---
title: Hexo Server Auto Restart
date: 2016-10-19 00:59:23
tags:
- Hexo
- Nodemon
---

## Introduce Hexo Auto Restart
Hexo is a great blog platform, the article you are looking right now is written on top of Hexo. If you tired manually to `Ctrl + c` start and restart server, you probably want two console window, one runs `hexo server -s`, `-s` means only serve static html files, which located at `public/` folder, and the other one runs `hexo generate --watch`, it's builtin command to watch file updates and auto generate new static files. Start those two commands, refresh your browser and you should see the new updates.

## Problem With Watch in VagrantBox
I personally had pretty much all developing projects running in the vagrant box, the problem of `hexo generate --watch` seems like doesn't corporate with vagrant box, so the [Nodemon](https://github.com/remy/nodemon) comes into the game.

## Install Nodemon
I prefer install Nodemon globally, `[sudo] npm install -g nodemon`, but if you don't like it, just do `npm install nodemon`

## Magic Command
Command: `nodemon -e html,md,less --ignore public/ -L --exec 'hexo generate'`, The Nodemon will start watching file updates and automatically runs `hexo generate`

Short explanation:
 - `-e` is adding the specific extension to Nodemon watch list, nodemon default looks for files with `.js`, `.coffee`, `.litcoffee` and `.json`, on this example, Nodemon will watch `.html`, `.md`. Add whatever extensions you want.
 - `-L` is only required if you running your developing environment on virtual machine, such as Vagrant, VirtualBox.
 - `--ignore public/` is important, otherwise, once you generated new static files, Nodemon will detect updates in public folder and start generate again, infinite loop...
 - `--exec 'hexo generate'` is the main command let Nodemon knows how suppose it to execute the program, inside `hexo server`, you can change it to whatever you currently using, for more information, check at [Hexo Server](https://hexo.io/docs/server.html)

## Finally
On production, you could consider to use [forever](https://github.com/foreverjs/forever) to start Hexo daemon, the command I use is
```
forever start --uid blog --append -c 'hexo server -s' ./
```
After you get new blog and pull from upstream, run `hexo generate` and your blog should get updated.