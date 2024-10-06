# *Abstract*
*When we want to deploy an app, we tend to follow some steps. Those steps are usually the dependency packages ─ install and maintenance. Furthermore, we do end up for install our target application software.*

*An application software deployment comes with a panoply of settingly behaviors, as long as a proper configuration set.*

*The very first step in order to gain control of our needs, it's to place a manual deployment ourselves.*

# 1. Introduction
For this lesson we'll take an open-source application, it's called "Swap". Its intend it is to be a manager for the student schedules, as long as the teachers schedules. Find more information about it on https://github.com/Hackathonners/swap .

# 2. Pre-requisites
For this particular deployment task, we need the providence of 2 virtual machines from our IaaS provider.

We'll work with node1, ```192.168.56.101```, and node2, ```192.168.56.102```.

For the matter of this deployment, it's all we have to know.
> *Hey, do you remeber what you have to do in order to provide our deployment ambience?* [Of course I do!](Cloud-Computing-Applications-and-Services/0.CreateVMs_IaaS)

# 3. Deployment
For the deployment of our app, we decide to indulge it on two different machines.

The first machine it's intended to run the app database.
> ```192.168.56.101```

The second machine it is intended to run the http app requests.
> ```192.168.56.102```

## 3.1 Database
Remember that this is a practice to load an empty machine. It has its Operative System, and nothing more.

### Install MySQL Server
Straightforward.
```
sudo apt install mysql-server
```

### Create, and manage the Swap database
Lunch the mysql server app.
```
sudo mysql
```

Manage to create the desired database.
```
CREATE DATABASE swap;
```

Open the database to a specific user, from a specific machine.
```
CREATE USER 'miguel'@'192.168.56.102' IDENTIFIED BY 'passinhas';
```
> ```miguel``` stands for my username;
> 
> ```192.168.56.102``` stands for the machine that will run the http requests;
> 
> ```passinhas``` stands for my password.

Work on its privileges.
```
GRANT ALL PRIVILEGES ON swap.* TO 'miguel'@'192.168.56.102' WITH GRANT OPTION;
```

### Configure the database
State where the requests shall be listened...

Open the following file with a bash editor.
```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
Search through the following configuration, and state that this node will be responsible to listening database requests.
```
bind-address            = 192.168.56.101
```
> ```192.168.56.101``` stands for the machine that will run the mysql dtabase requests.

Make it count.
```
sudo /etc/init.d/mysql restart
```

## 3.2 App
In order to understand its requirements, we shall read the authors README. We can find that in the public repository: https://github.com/Hackathonners/swap .

There, it states the following set of requirements [^1]:
- PHP 7.4+;
- PostgreSQL;
- Composer;
- NodeJS;
- Yarn.

Moreover, the preceding README document, states how the Swap installation, as long as its configuration shall be made.

### PHP
Add the ondrej repository to the pull of repositories.
```
sudo add-apt-repository ppa:ondrej/php
```

Update our pull.
```
sudo apt update
```

Don't ask, I don't tell.
```
sudo apt install php7.4 \
php7.4-{fpm,zip,mbstring,tokenizer,mysql,gd,xml,bcmath,intl,curl}
```

### NodeJS and npm
Let's go.
```
sudo apt install nodejs npm
```

### Composer-v1
Start by fetching and install the binary.
```
curl -sS https://getcomposer.org/installer | php -- --1
```
End it by placing it where it should be.
```
sudo mv composer.phar /usr/bin/composer
```

### 3.2.1 Install
Fetch the open-source repository app.
```
git clone https://github.com/Hackathonners/swap.git
```
Enter the swap directory ```cd swap```, and run the package required management installation.
```
composer install
```
Finally, install the Swap application.
```
npm install
```

### 3.2.2 Configure
The Swap team provided us with an ```.env.example```. Here it is stated all the possible stand-alone configurations.

Open it with a bash editor.
```
sudo vi .env.example
```
Configure the following variables (infra descriminated). Place your configurations. Pay attention to the ```DB_HOST```, it shall indicate the machine that will run the mysql database requests.
```
DB_HOST=192.168.56.101
DB_DATABASE=swap
DB_USERNAME=miguel
DB_PASSWORD=passinhas
```
For the app to recognize the ```.env``` file, it is necessary to padronize it ─ rename it.
```
mv .env.example .env
```

In order to establish secure connections/communications, generate the Swap app key.
```
php artisan key:generate
```

Set up the database, as follows:
```
php artisan migrate
```
, and place it with some example data content.
```
php artisan db:seed
```

Start the service! 😊
```
php artisan serve --host=0.0.0.0
```

### 3.2.3 Web Browser
The final test... 🤭

Go to your web browser and connect to the following URl: http://192.168.56.102:8000 .

Attempt to login as administrator:

> username: ```contact@hackathonners.org```
> 
> password: ```123456```

*Did you deploy?*

[^1]: Swap installation requirements from https://github.com/Hackathonners/swap?tab=readme-ov-file#requirements .
