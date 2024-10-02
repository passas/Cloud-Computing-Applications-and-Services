## 0. The Cloud environment
My pc.

| Spec. |        Detail         |
| :---  |        :---:          |
| OS    | Ubuntu 24.04.1 LTS    |
| CPU   | Intel® Core™ i3-9100F |
| RAM   | 16.0 GiB              |

## 1. The goal of our Infrastructure
Use Vagrant to create and configure 5 VMware virtual machines.

![](assets/media/diagrams/goal_0.png)

### 1.1. VMware installation
#### 1.1.1. Register
Register yourself at [Broadcom Registration](https://profile.broadcom.com/web/registration).

#### 1.1.2. Download
Workstation Pro 17.0 for Personal Use.
> Choose the most recent version.

a) Download at [Broadcom VMware](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Workstation+Pro);

b) Install.

```
$ chmod +x <file>

$ sudo ./<file>
```


### 1.2. Vagrant installation
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
