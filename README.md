# Connect to Docker on Ubuntu VM Hyper-V

How connect DB2 via DBeaver to Docker using an Ubuntu VM installed on Hyper-V.

> **Note:** This **is not a recommended practice**, but if you need to use Window OS and Docker doesn't work on Windows, this can also be a possible "solution" for you too, it's worked for me, in which  I managed to create.

### Contents
- [1. Hyper-V networking Settings](#1-hyper-v-networking-settings)

## Steps:

### 1. Hyper-V networking Settings
Install a normal Ubuntu VM and, after installation, use the 2 networks settings as the images is showing below. This is necessary because you need an Internet network and a static network to connect to a host database DB2, thus avoiding having to change the host every time you log into Ubuntu.

> PS: In the new versions of Hyper-V, you can install Ubuntu directly in the installation settings, without needing the ISO image, see more about it by: <a href="https://blogs.windows.com/windowsdeveloper/2018/09/17/run-ubuntu-virtual-machines-made-even-easier-with-hyper-v-quick-create/" target="_blank">clicking here</a> <i>(Last access: 2020-03-15).</i>

- 1.1. MAC Address - The MAC address must be static for both networks in Hyper-V

<i>Static MAC Address 1</i>
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.1.0.png" class="center">

<i>Static MAC Address 2</i>
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.1.1.png" class="center">

- 1.2. On Ubuntu, get the second network with the shell and the command ```ifconfig```, then keep the IP static as the image shows below:
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.2.0.png" class="center">

You can see on Windows with the command:
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.2.1.png" class="center">

And See the on Hyper-V Tab Network:
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.2.2.png" class="center">
