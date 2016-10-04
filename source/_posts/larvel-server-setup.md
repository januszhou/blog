---
title: Laravel Sever Setup On EC2
date: 2016-10-04 20:43:28
tags:
- server-setup
- EC2
- Laravel
---
## Laravel Server Setup
Environment setup on EC2, Linux ubuntu 14.04 + php 5.6 + mysql 5.7 + apache 2.4

### PHP

``` bash
sudo apt-get -y update
sudo add-apt-repository ppa:ondrej/php
sudo apt-get -y update
sudo apt-get -y install php5.6 php5.6-mcrypt php5.6-mbstring php5.6-curl php5.6-cli php5.6-mysql php5.6-gd php5.6-intl php5.6-xsl
```

### Git & Zip
``` bash
sudo apt-get install zip unzip git
```

###Mysql 5.7
```
wget http://dev.mysql.com/get/mysql-apt-config_0.6.0-1_all.deb
sudo dpkg -i mysql-apt-config_0.6.0-1_all.deb
sudo apt-get update
sudo apt-get install mysql-server mysql-client
then select 5.7
```

###Redis
```
sudo add-apt-repository ppa:chris-lea/redis-server
sudo apt-get update
sudo apt-get install redis-server
```

### Composer
Follow instruction on [website](https://getcomposer.org/download/), then

```
mv composer.phar /usr/local/bin/composer
```

### Apache
```
sudo a2enmod rewrite
sudo service apache2 restart
```

###Install Laravel dependencies
```
composer install
chmod 777 bootstrap/cache
chmod 777 -R storage
```



