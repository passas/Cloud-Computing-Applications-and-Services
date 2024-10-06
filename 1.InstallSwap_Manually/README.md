# Abstract
When we want to deploy an app, we tend to follow some steps. Those steps are ussually the dependency packages, install and maintenance. Furthermore, we do install our target application software.

An application software deployment comes with a panoply of setting behaviors, as long as proper configuration.

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

The first machine is intended to run the app database.
> ```192.168.56.101```

The second machine is intended to run the http app requests.
> ```192.168.56.102```

## 3.1 Database
Remember that this is a practice to load an empty machine. It has its Operative System, and nothing more.

### Install MySQL Server
Straightforward.
```
sudo apt install mysql-server
```
