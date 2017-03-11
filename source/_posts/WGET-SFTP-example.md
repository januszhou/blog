---
title: Wget & SFTP Examples
date: 2017-03-01 22:57:47
tags:
- WGET
- SFTP
---

## Story
My company needs grab files from 3rd party servers daily and only today's file. Here are useful snippets of FTP and SFTP.

## Wget From FTP
If you need `wget` download specific file from another server, there is accept list argument `-A` that helps us filter today's file.

```
today=$(date +"%Y-%m-%d")
wget --user='ROOT' --password='PWD' -r --no-parent -A "File $today*" ftp://ftp.server.com/ -O ./destination.csv
```

## SFTP
For SFTP, once you have public key installed on their server, you can do the following
```
today=$(date +"%Y-%m-%d")
sftp name@server.com <<EOF
get *$today* destination.csv // name the file as destination.csv
quit
EOF
```
