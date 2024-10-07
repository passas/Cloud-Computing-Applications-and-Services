# 1. Introduction
In this directory we'll intend to create, and run 2 containers simultaneosly. One for the database, and the other for the app itself.

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

Create a docker group.
```
sudo groupadd docker
```

Add our user to the docker group.
```
sudo usermod -aG docker $USER
```

Re-evaluate the group membership.
```
newgrp docker
```

And *voilà*!


[^4]: How to install Docker: https://docs.docker.com/engine/install/ubuntu/ .

[^5]: How to remove sudo from the docker commands: https://docs.docker.com/engine/install/linux-postinstall/ .
