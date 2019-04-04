# Magento2.3 (Nginx + PHP7.2fpm + Mysql + Phpmyadmin +Redis + RabbitMQ)

#### Docker is a tool that is use to create virtual container and run the application over that in OS Level.

#### Docker compose is a tools with that multiple docker containers can be run at a time.
#### In this repository we create multiple containers that are required to run Magento 2.3 like Nginx + PHP7.2fpm + Mysql

#### To use this you just need to install "docker" and "docker compose".

# Steps to Deploy.

## Clone this repositary

```
git clone git@github.com:KrishaWeb/docker-magento23-lemp.git
```
## Go to the directory that you have extracted.


## Downloading Magento2.3
```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition public
```

## Do you want sample data?
Execute (from the host machine):
```
cd public
php bin/magento sampledata:deploy
composer update
```
You can lunch the same commmands from within the container, it's actually the same thing

## Starting all docker containers
```
docker-compose up -d
```
The fist time you run this command it's gonna take some time to download all the required images from docker hub.

## Install Magento2.3

open your browser to the address:
```
http://magento2.docker/
```
and use the wizard to install Magento2.  
For database configuration use hostname dockermagento2_db_1 and username/password/dbname you have in your docker-compose.xml file, defaults are:
- MYSQL_HOST=mysql
- MYSQL_USER=root
- MYSQL_PASSWORD=root
- MYSQL_DATABASE=magento2

## Deploy static files
```
docker exec -it magento23docker_phpfpm bash
php bin/magento dev:source-theme:deploy
php bin/magento setup:static-content:deploy
```

and delete all Magento's cache with
```
rm -rf public/var/cache/*
```
from now on the var/cache directory should stay empty cause all the caches should be stored in Redis.


## RabbitMQ
The Docker official RabbitMQ image is included.
You can use _rabbitmqctl_ via _docker exec_, for instance to see the list of defined queues you just need to execute the following command:
```
docker exec -it magento23docker_rabbitmq rabbitmqctl list_queues
```

# Links

Web : http://localhost:3000/

PhpMyAdmin : http://localhost:8186/

##Mysql Data
User  : root
Password : root
Host : mysql
Database  : magento2