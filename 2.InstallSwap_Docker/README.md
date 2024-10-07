# 1. Introduction

In this lesson we will take a more suitable approach to the matter of the app deployment itself.

Nowadays, in order to deploy an application, its deployment follow a containerized form. In this containerized form, the DevOp writes a standalone script in order to get the application ongoing, with all it's dependencies ─ requirments.

Nonetheless, this isn't enough. The DevOp shall (1) certificate that, in fact, the Docker software is installed in the machine, and (2) apply some configurations, which lead to further tasks that a container can not support. It is where Ansible software come along.

Ansible is a tool to take care of all the previous and post orchestration required through the deployment intervenience besides the container image itslef.

## 1.1. Container
A container it is the most lightweight form of environment in order to run an application in its independent self form [^1]. A container feeds himself from the host machine (operative system, and hardware) [^1].

Appart from that, the container context is uniquely known to itself [^2]. Two containers in the same host, know nothing about each others existence ─ that both are hosted in the same host machine, what's the amount of resource consumption from each other, their context, etc.

## 1.2. Docker
"(...) Run anywhere."

Docker is a tool that is used to automate the deployment of applications in lightweight containers so that applications can work efficiently in different environments in isolation [^3]. 

## 1.3. Ansible
<!--## 1.3 Ansible <img src="media/ansible1.png" width="28">-->
*Learning...*

# 2. Pre-requisites
In order to complete this lesson, we'll need two virtual machines from our provider.

For the case, node1, ```192.168.56.101```, and node2, ```192.168.56.102```.

## 2.1. Docker
For this lesson, our IaaS provider shall take the following providences.

### Install
From the Docker website, our IaaS provider shall be able to manage its deal [^4].

Set the proper apt repository.
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install the packages.
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

And that's it.

### Sudo
In order for the canambert to take place, we will remove the need for ```sudo``` authentication, as leadind in the documentation [^5].

<hr>

### References

[^1]: The Docker webpage, at "What is a container?" resources. Accessed from https://www.docker.com/resources/what-container/ .

[^2]: "What is a container?", p.7 from "Guide 2 Docker & Ansible", 2024-2025.

[^3]: The Docker (Software) Wikipedia page: https://en.wikipedia.org/wiki/Docker_(software) .

[^4]: How to install Docker: https://docs.docker.com/engine/install/ubuntu/ .

[^5]: How to remove sudo from the docker commands: https://docs.docker.com/engine/install/linux-postinstall/ .
