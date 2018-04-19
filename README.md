#Instructions on How to Run the Demo
##Tutorial of Installation

###Installation Steps
#####1.Xen Installation
#####2.VM Creation
#####3.Hadoop Installation
#####4.Spark Installation
#####5.Hive Installation
---
###1.Xen Installation


First of all, enter these command to upgrade your environment.

```
sudo apt-get update

sudo apt-get upgrade
```

Then Install a 64-bit Xen-hypervisor

`sudo apt-get install xenhypervisor-amd64`

Type “Y” for confirmation if asked

 Install vim (Vi Improved, recommend). Should be installed already
 
`sudo apt-get install vim`

#####Configure GRUB to start Xen

`sudo vim /etc/default/grub`

|Before  |         After         |
|-------|:------------------------------:|
|GRUB_DEFAULT=0 | GRUB_DEFAULT=**"Xen 4.4-amd64"**    |
| GRUB_HIDDEN_TIMEOUT=0   |  **#**GRUB_HIDDEN_TIMEOUT=0      |
|GRUB_CMDLINE_LINUX=""|GRUB_CMDLINE_LINUX=**"rebootdelay=100"**|

Save changes and update.

`sudo update-grub`

#####Network configuration

`sudo vim /etc/network/interfaces`

|Before  |         After         |
|-------|:------------------------------:|
|iface eth0 inet dhcp|iface eth0 inet **manual**   |
Adding below. (Be carefull, the third line starts with a TAB)
```
auto xenbr0
iface xenbr0 inet dhcp
    bridge_ports eth0
```
Save changes then reboot

`sudo reboot`

After reboot, check the network.

`sudo xl list`
You should see **Domain-0** is running

#####Install Xen Utilities

`sudo apt-get install xen-utils-4.4 xenwatch xen-tools xen-utils-common
xenstore-utils virtinst virt-viewer virt-manager`

Type “Y” for confirmation

#####Hypervisor Configuration
`sudo vim /etc/xen/xend-config.sxp`

|Before  |         After         |
|-------|:------------------------------:|
|#(xend-unix-server no)|(xend-unix-server **yes**)|
Fianlize the settings
```
sudo mkdir /home/xen/
sudo chmod 777 -R /home/xen 
sudo ln -s /usr/lib/xen-4.4 /usr/lib/xen
```
---
###2.VM Creation

#####Set Default Virtual Machine Configuration
`sudo vim /etc/xen-tools/xen-tools.conf`

|Parameter  |         Value         |
|-------|:------------------------------:|
|dir | /home/xen    |
| size   |        50G         |
|memory| 4096MB (for 16GB Memory Machine) / 2048MB (for 8GB Memory Machine) |
|swap|8192MB|




|Parameter  |         Value         |
|-------|:------------------------------:|
|marked | markdown编译为html    |
| ace   |        编辑器         |
|||

