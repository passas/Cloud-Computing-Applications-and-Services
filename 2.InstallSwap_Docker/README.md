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
