# 1. Setup
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

*Test:*
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


# 2. Docker network
(In order for the containers to communicate with each other.)

**Create**
```
docker network create swap_network
```
*Confirm:*
```
docker network inspect swap_network
```


# 3. Database container

**Download an already pre-existing image**
```
docker image pull mysql:latest
```
*Confirm:*
```
docker image ls
```

**Run**
```
docker run --name swap_db --net swap_network -p 3306:3306 -d \
-e MYSQL_USER=miguel -e MYSQL_PASSWORD=passinhas \
-e MYSQL_DATABASE=swap -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
-v mysql:/var/lib/mysql \
mysql:latest
```
> `-e` stands for .env configs;
> 
> `-v` stands for a physical volume creation (for storage in this case).

*Confirm:*
```
docker volume ls
```
```
docker exec -i swap_db \
mysql -umiguel -ppassinhas <<< "SHOW DATABASES;"
```

<hr>

# 4. App container
*\*At your host machine, create the deployment Dockerfile...\**

**Copy the file to the node**
```
scp Dockerfile vagrant@192.168.56.101:.
```
