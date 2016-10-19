---
title: Hexo Server Auto Restart By Using Nodemon
date: 2016-10-19 00:59:23
tags:
- Hexo
- Nodemon
---

## Introduce Hexo + Nodemon
Hexo is a great blog platform, the article you are looking right now is written on top of Hexo. However, the only annoying part I found about on local developing is it doesn't watch file update, you need manually stop and restart the server to see your updates on browser. The solution I would prefer is go with [Nodemon](https://github.com/remy/nodemon)

## Install Nodemon
I prefer install Nodemon globally, `sudo npm install -g nodemon`, but if you don't like it, just do `npm install nodemon`

## Update package.json
Adding this snippet into your package.json.

Short explanation:
 - `-e` is adding the specific extension to Nodemon watch list, nodemon default looks for files with `.js`, `.coffee`, `.litcoffee` and `.json`, on this example, Nodemon will watch `.html`, `.md`.
 - `-L` is only required if you running your developing environment on virtual machine, such as Vagrant, VirtualBox.
 - `--exec 'hexo server'` is the main command let Nodemon knows how suppose it to execute the program, inside `hexo server`, you can change it to whatever you currently using, for more information, check at [Hexo Server](https://hexo.io/docs/server.html)

```
  "scripts": {
    "start": "nodemon -e html,md -L  --exec 'hexo server'"
  },
```

## Enjoy it
Now run `npm start`, and update any `md` file and save it, the Hexo server should get restarted automatically.
