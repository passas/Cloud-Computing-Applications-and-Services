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

### a) Create an authorized exterior access;
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

### b) Open #node1 mysql server;
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
