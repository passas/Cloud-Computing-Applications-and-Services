# 1. Intro
In this lesson we will take a more suitable approach to the matter of deployment itself.

Nowadays, in order to deploy an application, its deployment follow a containerized form. In this containerized form, the DevOp writes a standalone script in order to get the application ongoing, with all it's dependencies ─ requirments.

Nonetheless, this isn't enough. The DevOp shall (1) certificate that, in fact, the Docker software is installed in the machine, and (2) apply some configurations, which led to further tasks that a container can not support. It is where Ansible software come along.

Ansible is a tool to orchestration all the pre, and post required intervenience beside the container deplyment itself.

## 1.1 Container
A container it is the most lightweight form of environment in order to run an application in its independent self form. A container feeds himself from the host machine (operative system, and hardware). Appart from that, its context is uniquely known to himself [^1].


<!--References-->
[^1]: The Docker webpage, on its "What is a container?" resources. Accessed from https://www.docker.com/resources/what-container/ .
