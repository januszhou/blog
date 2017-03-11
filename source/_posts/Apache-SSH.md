---
title: Apache SSH
date: 2017-01-21 22:22:12
tags:
- Apache
- SSH
- PHP
---

## Test SSH under Apache role
If you need PHP to process bash script, and it need SSH to another server process something else. Example PHP snippet: `$bash = shell_exec('bash ./example.sh');`.

Because PHP running under Apache, so Apache needs SSH to correct server. However, Ubuntu prevent `su apache` for obvious security reason, but you still able to change it.
```
sudo vim /etc/passwd
```

After find role Apache, change `/sbin/nologin` to `/bin/login`. Now you can do `su apache`.

Under Apache role, test your SSH host, you need add host to your trust list for first time. You probably want create `ssh_config` file under `/var/www/`.

Don't forget update Apache to `/sbin/nologin` after it.
