# Abstract
When we want to deploy an app, we tend to follow some steps. Those steps are ussually the dependency packages ─ install and maintenance. Furthermore, we do end up for install our target application software.

An application software deployment comes with a panoply of settingly behaviors, as long as a proper configuration set.

The very first step in order to gain control of our needs, it's to place a manual deployment ourselves.

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

[^1]: Swap installation requirements from https://github.com/Hackathonners/swap?tab=readme-ov-file#requirements .
