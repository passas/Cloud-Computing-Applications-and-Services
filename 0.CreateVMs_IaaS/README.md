> [!IMPORTANT]
> This subject is not the intend of this Cloud Computing Applications and Services course.
>
> The work of providing an Infrastructure as a Service, it's of extremely professional demand. It is risky and unsafe. We do not encourage you to take further attempts as the didatic one.
>
> Moreover, we defend that if you can pay for an expertise to do the job, then you should.

# 1. Introduction
This directory is dedicated to the job of an Infrastructure as a Service, also known as, Clouds.

They provide for us specific and controlled resources, which are being distributed from a physical machine, or a network of ones.

From the panoply of virtualization softwares, we decided to go with the VirtualBox one. We have a section directory with one another, if you want to explore a more powerfull virtualizer one.

<hr>

# 2. VirtualBox
In order to procceed with our deeds, we need a software that can virtualize environments, moreover, we need a software whom virtualize machines.

We have (little) experience in working with both VMWare & VirtualBox.

Although we choose the VirtualBox here, we do have the chills when it comes to this software. Despite of being not much invasive as the VMWare software, it brings a little uncertainity on the Ssh communications protocol, and as a creating NATs concerns.

Before we proceed with our experiments, we did a lot of 'ups' and 'halts' just to test some behaviors of what we could expect during our app deployments via this particular software. So far, we did observe problems in 'up' vms, as we had to go into the VirtualBox software, shut down the VM, delete it, as all of its files, and then re-up the vms. On halt operations we did see a lot of "forcing shutdowns", so it's pretty clear that those virtualizations are not good if we want to endure our deployment trough it. For now, it's enough!

## 2.1. Pre-requisites
The VirtualBox software intends to have some libraries pre-installed in the host machine.
```
sudo apt-get update 

sudo apt-get install build-essential gcc make perl dkms

reboot
```

## 2.2. Download
Since the Vagrant software can run up to the VirtualBox 7.0 version, we have to download that older version [^1]. For more older versions, consult: https://www.virtualbox.org/wiki/Download_Old_Builds .


## 2.3. Installation
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

# 3. Vagrant

[^1]: VirtualBox v7.0 https://www.virtualbox.org/wiki/Download_Old_Builds_7_0 .
