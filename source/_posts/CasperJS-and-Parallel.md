---
title: CasperJS and Parallel
date: 2017-02-11 20:50:24
tags:
- CasperJS
- Parallel
- PhantomJS
---
## Trouble on CasperJS
One of the project we need use [CasperJS](casperjs.org) to navigates dozens URLs, evaluate hundreds lines of javascript in that page then submit the form, sounds crazy right?! <!-- more -->

Unfortunately, even we tried our best to optimize the page loading performance, the whole process is take around one hour. We tried initialize multiple instances of CasperJS and running those at same time, but it still failed. 

However, we found this [blog](http://g-liu.com/blog/2016/10/tutorial-parallel-web-scraping-with-casperjs-and-gnu-parallel/), by utilizing Parallel, program ables to process CasperJS under multiple threads simultaneously, the following steps similar to that blog except I will list installation parts.

## Check CPU cores
Make sure your server has more than 1 core...

```
Mac: # sysctl -n hw.ncpu
Linux: # nproc
```

## Install CasperJS
```
// install phantoms 2.1.1
# wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
# tar xvf phantomjs-2.1.1-linux-x86_64.tar.bz2
# cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin
# phantomjs -v
# 2.1.1
# npm install -g casperjs
```

## Install Parallel
```
cd /etc/yum.repos.d/
wget http://download.opensuse.org/repositories/home:/tange/CentOS_CentOS-6/home:tange.repo
yum install parallel
```

## Examples
Imagine you will need a list URLs like below and named as `list.txt`, or generate it by yourself.

```
https://google.com
https://yahoo.com
https://facebook.com
...
```

Then you can use the following command to process those URLs simultaneously.

```
parallel --bar -a list.txt casperjs process.js
```

## HTTP Redirect
If the URL is being forced redirect from http to https, you probably will get redirect and won't get anything, in this case, add `--ignore-ssl-errors=true --ssl-protocol=any` to your command.
