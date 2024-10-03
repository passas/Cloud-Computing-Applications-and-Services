## 0. The Cloud environment
My pc.

| Spec. |        Detail         |
| :---  |        :---:          |
| OS    | Ubuntu 24.04.1 LTS    |
| CPU   | Intel® Core™ i3-9100F |
| RAM   | 16.0 GiB              |

## 1. The goal of our Infrastructure
Use ***Vagrant*** to create and configure 5 ***VMware*** virtual machines.

![](assets/media/diagrams/goal_0.png)

## 2. Framework
We'll use the VMware, an hypervisor software, in order to create virtual machines. We'll also use Vagrant, a software to automatize the deployment of those virtual machines.
### 2.1. VMware installation
#### 2.1.1. Register
Register yourself at [Broadcom Registration](https://profile.broadcom.com/web/registration).

#### 2.1.2. Download
Workstation Pro 17.0 for Personal Use.
> Choose the most recent version.

a) Download at [Broadcom VMware](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Workstation+Pro);

b) Install.

```
$ chmod +x <file>

$ sudo ./<file>
```


### 2.2. Vagrant installation
```
$ sudo apt install vagrant
```

```
$ sudo apt install vagrant-vmware-utility
```

```
$ vagrant plugin install vagrant-vmware-desktop

$ vagrant plugin update vagrant-vmware-desktop
```

## 3. Deployment
Our cloud will communicate with the infrastructure through the ssh protocol.
### 3.1 Create the Cloud public key
```
$ ssh-keygen
```

<img src=assets/media/showcase/ssh_key.png width=720>

### 3.2 Inspect Vagrantfile
> *Take some time to explore the virtual machines deployment file.*

In the file, take special attention to these variables in which states the path for the ssh keys.
```
PUBLIC_KEY_PATH = "~/.ssh/id_ed25519.pub"
PRIVATE_KEY_PATH = "~/.ssh/id_ed25519"
READ_PUBLIC_KEY = File.read(File.expand_path(PUBLIC_KEY_PATH)).strip
```

### 3.3 Deploy
In the same directory as the vagrant file.

```$ vagrant up```
<img src="media/diagrams/infrastructure1.png">

### 3.4 Check-up
```$ vagrant status```


