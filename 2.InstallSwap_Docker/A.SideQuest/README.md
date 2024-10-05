# Sidequest #1

```
╔───────────────────────────────╗
║Docker: Put a container online.║
╚───────────────────────────────╝
```

# 1. Introduction
As you're familiar with unix shell comands, so do Docker have ones of their own.

In this tutorial [^1] it is important to observe how to use them in order to:

a) Build an image;

b) Put a container online;

c) Access a container shell;

d) Halt a container;

e) Remove a container.

## 1.1. Quest
### a) Build an image;
```
docker build -t <given-name> <path>
```

### b) Put a container online;
```
docker run -dp 192.168.56.101:3000:3000 getting-started
```

### c) Access a container shell;
```
docker ps

docker exec -ti <contianer id|name> /bin/sh
```

### d) Halt a container;
```
docker ps

docker stop <container>

docker start <container>
```

### e) Remove a container.
```
docker ps

docker rm <contaienr>
```


<!-- References -->
[^1]: Docker workshop, https://docs.docker.com/get-started/workshop/02_our_app/ .
