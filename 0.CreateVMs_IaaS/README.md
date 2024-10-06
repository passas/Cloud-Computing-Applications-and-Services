> [!IMPORTANT]
> This subject is not the intend of this Cloud Computing Applications and Services course.
>
> The work of providing an Infrastructure as a Service, it's of extremely professional demand. It is risky and unsafe. We do not encourage you to take further attempts as the didatic one.
>
> Moreover, we defend that if you can pay for an expertise to do the job, then you should.

# 1 Introduction
This directory is dedicated to the job of an Infrastructure as a Service, also known as, Clouds.

They provide for us specific and controlled resources, which are being distributed from a physical machine, or a network of ones.

From the panoply of virtualization softwares, we decided to go with the VirtualBox one. We have a section directory with one another, if you want to explore a more powerfull virtualizer one.

<hr>

# 2 VirtualBox <img src="media/assets/logos/Virtualbox_logo.png" width="42">
In order to procceed with our deeds, we need a software that can virtualize environments, moreover, we need a software whom virtualize machines.

We have (little) experience in working with both VMWare & VirtualBox.

Although we choose the VirtualBox here, we do have the chills when it comes to this software. Despite of being not much invasive as the VMware software, it brings a little uncertainity on the Ssh communications protocol, and as a creating NATs concerns.

Before we proceed with our experiments, we did a lot of 'ups' and 'halts' just to test some behaviors of what we could expect during our app deployments via this particular software. So far, we did observe problems in 'up' vms, as we had to go into the VirtualBox software, shut down the VM, delete it, as all of its files, and then re-up the vms. On halt operations we did see a lot of "forcing shutdowns", so it's pretty clear that those virtualizations are not good if we want to endure our deployment trough it. For now, it's enough!

## 2.1 Pre-requisites
The VirtualBox software intends to have some libraries pre-installed in the host machine.
```
sudo apt-get update 

sudo apt-get install build-essential gcc make perl dkms

reboot
```

## 2.2 Download
Since the Vagrant software can run up to the VirtualBox 7.0 version, we have to download that older version [^1]. For more older versions, consult: https://www.virtualbox.org/wiki/Download_Old_Builds .


## 2.3 Installation
The installation was intended to get done with the **dpkg** ubuntu software, as follows:
```
sudo dpkg -i <virtualbox.deb>
```
.

The team got some dependency packages in its way. The fixture tool could manage for us.
```
sudo apt --fix-broken install
```

Re-run the installation:
```
sudo dpkg -i <virtualbox.deb>
```
.

All good. The team also decided too rebuild the kernels.
```
sudo /sbin/vboxconfig
```

For the confirmation itself we runned the software via bash terminal.
```
virtualbox
```

All good!

<hr>

# 3 Vagrant
Vagrant is a software to automatize the deployment and configuration of virtual machines.

The installation process can follow 2 steps: (1) the installation of the software itself, and (2) the installation of a utility package, in case you use the VMware software in order to get your virtualizations.

## 3.1 Pre-requisites
For establish network connection, and network management in our virtual machines, we need to install the netstat tool.
```
sudo apt install net-tools
```

In order to establish communication, via ssh protocol, with the future virtual machines, we need to set up our ssh keys.
```
ssh-keygen
```
It's important to check the name of the files, private and public keys, as also where did they go.
> Usually as ```~/.ssh/id_rsa``` and ```~/.ssh/id_rsa.pub```.


## 3.2 Download & Installation
For the Vagrant software itself, you can run your installation by putting the following statements on your bash terminal:
```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant
```
.

Or, if you prefer, you can manage to do it mannually [^1].

## 3.3 Virtualization
For the virtualization itself, you shall pick a Vagrantfile.

For the purpose of this course, we attend you with one.

> [!WARNING]
> Stay tunned to the following lines:
> ```
> PUBLIC_KEY_PATH = "~/.ssh/id_rsa.pub"
> PRIVATE_KEY_PATH = "~/.ssh/id_rsa"
> ```
> ,as they state the public and private path for the ssh keys of yours.

### 3.3.1 Up
To manage the start of the automated VMs creation process, indulge it by the following command on the bash:
```
vagrant up
```
.

### 3.3.2 Halt
It's a gracefull shutdown.
```
vagrant halt
```

### 3.3.3 Destroy
When in need to re-deploy a VM, do the following command:
```
vagrant destroy <vmname>
```


### 3.3.4 Status
In order to check the VMs status, do the following command:
```
vagrant status
```

## 3.4 Tests
At this phase, in order to test the good deploytment of our desired VMs, you can do the following:

**node1**
```
ssh vagrant@192.168.56.101
```
**node2**
```
ssh vagrant@192.168.56.102
```
**myvm**
```
ssh vagrant@192.168.56.10
```
**monitor**
```
ssh vagrant@192.168.56.200
```
**control plane**
```
ssh vagrant@192.168.56.100
```

If something isn't coming along, try to ```destroy``` that one VM, and ```up``` it again.

<!--References-->
<hr>
<hr>

### References

[^1]: Vagrant installation guide, at https://developer.hashicorp.com/vagrant/install/vmware .


[^1]: VirtualBox v7.0 https://www.virtualbox.org/wiki/Download_Old_Builds_7_0 .
