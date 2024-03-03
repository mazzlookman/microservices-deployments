### Deployments:

#### 1. Create Ubuntu Linux Container
```shell
docker run -d -it -p 8080:80 --name api-gateway main-ubuntu-server
```

#### 2. Connect to Ubuntu container command line
```shell
docker exec -it --user root api-gateway /bin/bash
```

#### 3. Install NVM & PM2
NVM installation:
```shell
# update & upgrade all ubuntu packages 
apt update && apt-upgrade

# get the latest version curl
apt install curl

# install NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# pick up the nvm command
source ~/.bashrc

# download, compile, and install the latest release of node
nvm install node
```

PM2 installation:
```shell
# install pm2 as globally to use
npm i -g pm2
```

#### 4. Install MySQL & Nginx
MySQL installation:
```shell
# update ubuntu's packages
apt update

# install mysql
apt install mysql-server

# start mysql,
# if you use WSL on Windows, there are differences in commands
# read the link bellow:
# https://itslinuxfoss.com/fix-system-not-booted-systemd-as-init-system-pidcant-operate/
systemctl start mysql

# set the MySQL service to automatically start at boot
systemctl enable mysql

# run mysql secure installation, choose "yes" to all questions
mysql_secure_installation
```
Create administrator user:
```shell
# enter to mysql
mysql -uroot -p

# create user
CREATE USER 'user_name'@'localhost' IDENTIFIED BY 'password';

# grant access rights to user
GRANT ALL PRIVILEGES ON *.* TO 'user_name'@'localhost' WITH GRANT OPTION;

# exit
exit;
```

Nginx installation:
```shell
# get nginx
apt install nginx
```

#### 5. Install PHP & Composer
PHP installation:
```shell
# install few dependency packages before adding the repo
apt install software-properties-common

# add PPA package to provides the latest stable versions of PHP
add-apt-repository ppa:ondrej/php

# update ubuntu's packages
apt update

# install PHP 8.2 (:fpm is for nginx)
apt install php8.2-fpm

# show php version to ensure
php -v

# install the commonly used modules
apt install php8.2-{common,mysql,xml,xmlrpc,curl,gd,imagick,cli,dev,imap,mbstring,opcache,soap,zip,intl,bcmath} -y

# installed modules can be listed with the command:
php -m
```

Composer installation:
```shell
# download composer with wget
apt install wget
wget https://getcomposer.org/download/latest-stable/composer.phar

#install composer
chmod 755 composer.phar
# create composer standalone file
mv composer.phar /usr/local/bin/composer

# check
composer
```

#### 6. Create snapshot of ubuntu-server
```shell
# create snapshot
# syntax:
docker commit {container_id} {image_name}

# example:
docker commit 2bfcb1d49ed7 ubuntu-server
```