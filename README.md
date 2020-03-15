# Connect to Docker on Ubuntu VM Hyper-v

How connect via DBeaver to Docker using an Ubuntu VM installed on Hyper-V.

> **Note:** This **is not a recommended practice**, but if you need to use Window OS and Docker doesn't work on Windows, this can also be a possible "solution" for you too, it's worked for me, in which  I managed to create.

## Steps:

1. Install a normal Ubuntu VM and, after installation, use the Network settings as the images is showing below. This is necessary because you need an Internet network and a static network to connect to a host database DB2, thus avoiding having to change the host every time you log into Ubuntu.

> PS: In the new versions of Hyper-v, you can install Ubuntu directly in the installation settings, without needing the ISO image, see more about it by [clicking here](https://blogs.windows.com/windowsdeveloper/2018/09/17/run-ubuntu-virtual-machines-made-even-easier-with-hyper-v-quick-create/)

- 1.1. MAC Address - The MAC address must be static for both networks in Hyper-v
