# Abstract
Docker is a tool whom manages containers.

A container is instatiated by a script, in the docker environment it's called "Dockerfile". When the Dockerfile it is instantiated, it turns itslef into a docker image, and that image is the object who compounds a running container.

Docker have a lot of specificities, one of them it is its Network Manager.

# 1. Introdcution
In this assignment we want to build two different containers.

In one container we want to run solely our data-base. In the another one, we want to build & run our app application.

Those containers shall run in the same machine. Its connections shall be managed by the Docker Network Manager.

# 2. Pre-requisites
Those pre-requisites are intended to be managed by the IaaS itslef.

It consists on the proper installation[^1], and configuration[^2] of the Docker tool.

# 3. Docker Network
In order for the 2 contianers communicate with each other, we have to establish a docker network.
```
docker network create <swap network name>
```
> Check if it's created by running ```docker network list```.
>
> Moreover, for further inspection you can manage the ```docker network inspect <swap network name>``` command.

# 4. MySQL container
Docker have its own reportory of pre-build images. As MySQL being one of them, we'll pull it, and start manage our database from their.
```
docker image pull mysql:latest
```
> Hey! Check out if the pull was been able to manage by running
> 
> ```docker image ls```
> 
> .

## 4.1 Configure
In order to configure the container, we shall adjust the following settings to our needs.
```
docker run --name <DB_CONTAINER_NAME> --net <NETWORK_NAME> -p 3306:3306 -d \
-e MYSQL_USER=<DB_USERNAME> -e MYSQL_PASSWORD=<DB_PASSWORD> \
-e MYSQL_DATABASE=<DB_DATABASE> -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
-v mysql:/var/lib/mysql \
mysql:latest
```
> The ```-v``` option stands for the mounting volume (storage).
>
> Check if it's mounted by running ```docker volume ls```.
>
> Moreover, you can run mysql commands as is:
> ```
> docker exec -i <DB_CONTAINER_NAME> mysql -u<DB_USERNAME> -p<DB_PASSWORD> <<< "SHOW DATABASES;"
> ```
> .

# 5. Swap container
We do need to create a Dockerfile from scratch. We have its documentations for support, start at: https://docs.docker.com/reference/dockerfile/ .

## 5.1 Clone the app repository
In order to build our app container, we shall clone its repository. Furthermore, the Dockerfile will be ment to set up straight to our app folder. Moreover, the Dockerfile will handle all the dependencies from our Swap app.
```
git clone https://github.com/Hackathonners/swap.git
```





[^1]: Install Docker on Ubuntu: https://docs.docker.com/engine/install/ubuntu/#installation-methods .
[^2]: Remove the need for sudo at Docker requests: https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user .
