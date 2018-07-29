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
mv symfony3 www/
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
<br/>ENJOY !

Access to PhpMyAdmin
-
You can access phpmyadmin from the url: ```http://symfony3.localhost:8001```
* _Username: dev_
* _Password: dev123_

Show docker processes
-
You can view the docker processes by running the following command line:
```
docker ps
```
Command output:
```
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                            NAMES
24ed5a4d0dd4        docker-symfony3_php     "docker-php-entrypoi…"   7 minutes ago       Up 7 minutes        9000/tcp                         docker-symfony3_php7
597e3309cb11        nginx:latest            "nginx -g 'daemon of…"   7 minutes ago       Up 7 minutes        0.0.0.0:80->80/tcp               docker-symfony3_nginx
8be703d965eb        mariadb:latest          "docker-entrypoint.s…"   7 minutes ago       Up 7 minutes        0.0.0.0:3306->3306/tcp           docker-symfony3_mariadb
b52749bfd3fd        phpmyadmin/phpmyadmin   "/run.sh phpmyadmin"     7 minutes ago       Up 7 minutes        9000/tcp, 0.0.0.0:8001->80/tcp   docker-symfony3_pma
```


Access to a container
-
You can access your container via the command line:
```
docker exec -it CONTAINER_NAME bash
```

Example: to access the php7 container
```
docker exec -it docker-symfony3_php7 bash
```

Note
-
* Stop containers by running the following command:
```
docker-compose stop
```

* After the modification of the configuration, rebuild containers by running the following command:
```
docker-compose build
```



