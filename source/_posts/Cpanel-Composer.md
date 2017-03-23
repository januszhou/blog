---
title: Cpanel Composer
date: 2017-03-23 22:06:39
tags:
---

## Cpanel suhosin issue
If you use cpanel and suhosin, you might get error

<!-- more -->

```
The suhosin.executor.include.whitelist setting is incorrect.
Add the following to the end of your `php.ini` or suhosin.ini (Example path [for Debian]: /etc/php5/cli/conf.d/suhosin.ini):
    suhosin.executor.include.whitelist = phar
```

You have two options to solve it, one is update `php.ini` file if you have the permission, the other one is add `-d` option as `php -d suhosin.executor.include.whitelist=phar` every time you need composer.

## Steps
The following code will do the work on 2nd method
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php -d suhosin.executor.include.whitelist=phar composer-setup.php
php -r "unlink('composer-setup.php');"
```
Then you can start enjoy composer

```
php -d suhosin.executor.include.whitelist=phar /path/to/composer.phar install
```
