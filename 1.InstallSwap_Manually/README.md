# 1. The installation Goal

![](media/assets/diagrams/goal.png)

## 1.1. Cloud provider
```
$ sudo systemctl start vagrant-vmware-utility

$ vagrant up node1 node2
```

# 2. Database Deploy
Connect to the Cloud VM.
```
$ ssh vagrant@192.168.56.101
```

## 2.1. Install MySQL
```
$ sudo apt install mysql-server
```

## 2.2. Launch MySQL
```
$ sudo mysql
```

## 2.3. Configure the database

### a) Create;
```
CREATE DATABASE swap;
```

### b) Create an authorized exterior access;
> CREATE USER '&lt;USER&gt;'@'&lt;IP>'&gt;IDENTIFIED BY '&lt;PASS&gt;ORD>';
>
> GRANT ALL PRIVILEGES ON swap.* TO '&lt;USER&gt;'@'&lt;IP>'&gt;WITH GRANT OPTION;


> [!CAUTION]
> 
> The IP stands for the machine where the user can sign in himsel; as the VM#node1 where the app will be further installed.
```
CREATE USER 'miguel'@'192.168.56.102' IDENTIFIED BY 'passinas';
GRANT ALL PRIVILEGES ON swap.* TO 'miguel'@'192.168.56.102' WITH GRANT OPTION;
```

### c) Open #node1 mysql server;
```
$ sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf 
```

```
bind-address = 192.168.56.101
```

```
sudo /etc/init.d/mysql restart
```

## 2.4. Test the database
At #node2 ```ssh vagrant@192.168.56.102```, do the following commands:

```
sudo apt install mysql-client

sudo mysql -u'miguel' -p'passinhas' -h '192.168.56.101' <<< "SHOW DATABASES;"
```
If you see the swap database as an output, you're ok!


# 3. App Deploy
```
$ ssh vagrant@192.168.56.102
```
## 3.1. Dependencies

### a) PHP;
```
$ sudo add-apt-repository ppa:ondrej/php

$ sudo apt update

$ sudo apt install php7.4 \
php7.4-{fpm,zip,mbstring,tokenizer,mysql,gd,xml,bcmath,intl,curl}
```

### b) NodeJS, npm, and Composer-v1.
```
$ sudo apt install nodejs npm

$ curl -sS https://getcomposer.org/installer | php -- --1

$ sudo mv composer.phar /usr/bin/composer
```

## 3.2. Swap

### Install

#### a) Clone the repo;
```
$ git clone https://github.com/Hackathonners/swap
```

#### b) Install packages;
```
$ cd swap

$ composer install
```

#### c) Install app
```
$ npm install
```

### Configure

#### a) Database;
```
$ sudo vi .env.example
```

```
DB_HOST=192.168.56.101
DB_DATABASE=swap
DB_USERNAME=miguel
DB_PASSWORD=passinhas
```

```
$ sudo mv .env.example .env
```

#### b) Key;
```
$ php artisan key:generate
```

#### c) Migrate;
```
$ php artisan migrate
```

#### d) Seed (with examples);
```
$ php artisan db:seed
```

#### e) Start.
```
$ php artisan serve --host=0.0.0.0
```

# 4. Web Browser
At your pc, access ```http://192.168.56.102:8000```.

Then try use those credentials, username ```contact@hackathonners.org```, and password ```123456```.
