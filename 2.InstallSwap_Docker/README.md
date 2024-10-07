# *Abstract*

*In this lesson we will take a more suitable approach to the matter of the app deployment itself.*

*Nowadays, in order to deploy an application, its deployment follow a containerized form. In this containerized form, the DevOp writes a standalone script in order to get the application ongoing, with all it's dependencies ─ requirments.*

*Nonetheless, this isn't enough. The DevOp shall (1) certificate that, in fact, the Docker software is installed in the machine, and (2) apply some configurations, which lead to further tasks that a container can not support. It is where Ansible software come along.*

*Ansible is a tool to take care of all the previous and post orchestration required through the deployment intervenience besides the container image itslef.*

## 1.1 Container
A container it is the most lightweight form of environment in order to run an application in its independent self form [^1]. A container feeds himself from the host machine (operative system, and hardware) [^1].

Appart from that, the container context is uniquely known to itself [^2]. Two containers in the same host, know nothing about each others existence ─ that both are hosted in the same host machine, what's the amount of resource consumption from each other, their context, etc.

## 1.2 Docker
<!--## 1.2 Docker <img src="media/docker1.png" width="48">-->
*Learning...*

## 1.3 Ansible
<!--## 1.3 Ansible <img src="media/ansible1.png" width="28">-->
*Learning...*

# 2. IaaS
> ```sudo systemctl start vagrant-vmware-utility```

In this section we indulge the cloud side of this deployment process.

At this stage we state that the #node1 it's our target vm for this deployment process. And so it comes the pre-set of it.

We, as IaaS, we'll integrate in our #node1 the Docker software [^3].

After reach our node ```ssh vagrant@192.168.56.101```, we took the dokcer app installation [^4] and remove its sudo permission request necessity [^5]. Notice that this follows a nonautomated path.

# 3. DevOp
We pre-negotiate the contract with our IaaS provider. It gaves us an address IP ```192.168.56.101``` where we could deploy our Swap application.

## 3.1. Swap application
Our swap application have 2 main components, the database component, and the app itself.

Moreover, we'll want to build each one of the components in a different container.

In order for both containers get to communicate with each other, we have to manage it through a Docker Network.

### 3.1.1. Docker Network
This process is really straightforward. More about it can be consulted in the Docker network drivers page [^6].

First we state a network.
```
docker network create <network name>
```

Then we check if it is really created.
```
docker network list
```

For some more advanced features, as DNS like configuration, we can inspect it.
```
docker network inspect <network name>
```

### 3.1.2. Database
For the database we'll instantiate a proper container, different from the one who will run the app itself.

As for Docker containers are about, we need to build an image. In this case, the Docker company already have one [^7].

This image refers to a mysql container, and comes with some mysql settings configuration on the moment of the container creation.

<!--References-->
<hr>

<!--<img src="media/ansible1.png" width="52"> <img src="media/docker1.png" width="72">  <img src="media/ansible1.png" width="52"> <img src="media/docker1.png" width="72">  <img src="media/ansible1.png" width="52"> <img src="media/docker1.png" width="72">  <img src="media/ansible1.png" width="52">-->

<hr>

### References

[^1]: The Docker webpage, at "What is a container?" resources. Accessed from https://www.docker.com/resources/what-container/ .

[^2]: "What is a container?", p.7 from "Guide 2 Docker & Ansible", 2024-2025.

[^3]: The Docker software: https://docs.docker.com/ .

[^4]: Docker installation, at https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository .

[^5]: Docker, remove sudo authentication from it, at https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user .

[^6]: Docker netword drivers documentation, at https://docs.docker.com/engine/network/drivers/ .

[^7]: MySQL Docker image: https://hub.docker.com/_/mysql .
