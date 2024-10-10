# Setup
**Connect to a node**
```
ssh vagrant@192.168.56.101
```

**Install Docker**
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

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**Remove sudo**
```
sudo groupadd docker
```

```
newgrp docker
```

*Test*
```
docker run hello-world
```

**Boot docker on startup**
```
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

*Stop the behavior*
```
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```


# Docker network
(In order for the containers to communicate with each other.)

**Create**
```
docker network create swap_network
```
*Confirm*
```
docker network inspect swap_network
```


# Database container
