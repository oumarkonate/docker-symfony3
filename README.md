DOCKER-SYMFONY3
==
SYMFONY3 applications using: &nbsp;Nginx, &nbsp;PHP7-FPM, &nbsp;PhpMyAdmin, &nbsp;MariaDB
<br/>
Docker compose file: version 3
<br/>
PHP Extension: memcached, opcache, pdo_mysql, gd, iconv, mcrypt, intl, mbstring, curl, zip, json, xdebug

Installation
-
* First, clone this repository: 
```
git clone https://github.com/oumarkonate/docker-symfony3.git
```

* Next, install composer into root directory ```docker-symfony3```: 
```
cd docker-symfony3
```
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
See the following link for manual download: ```https://getcomposer.org/download/```

* Next, install your symfony3 application. Run the following command into root directory ```docker-symfony3```: 
```
composer create-project symfony/framework-standard-edition symfony3 "3.4.*"
```

* Next, move your symfony3 application into directory ```www```:
```
mv symfony3 www/symfony3/
```

* Next, change permission of directory ```www```:
```
chmod -R 777 www/
```
<br/>In production environment, it is strongly discouraged to give permission 777. Give the minimum permission to folders and files.

* Next, add the following line in file /etc/hosts:
```
127.0.0.1 symfony3.localhost www.symfony3.localhost
```
Restart the network service by the command:
```
/etc/init.d/networking restart
```

* Then, go to folder ```docker-symfony3``` and run:
```
docker-compose up -d
```

* Go to the application on the following url: ```http://symfony3.localhost```

