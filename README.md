# Connect DB2 via DBeaver to Docker on Ubuntu VM Hyper-V

How connect DB2 via DBeaver to Docker using an Ubuntu VM installed on Hyper-V.

> **Note:** This **is not a recommended practice**, but if you need to use Window OS and Docker doesn't work on Windows, this can also be a possible "solution" for you too, it's worked for me, in which  I managed to create.

### Contents
- [1. Hyper-V networking Settings](#1-hyper-v-networking-settings)
- [2. Installing DB2 on the Docker](#2-installing-db2-on-the-docker)
- [3. Connecting DB2 on Docker with DBeaver](#3-connecting-db2-on-docker-with-dbeaver)
- [4. Reference](#4-reference)
- [5. About](#5-about)

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

You can see in Windows with the command ```arp -a <ip-address>```:
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.2.1.png" class="center">

And see the network settings on the Hyper-V Networking tab:
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/1.2.2.png" class="center">

### 2. Installing DB2 on the Docker
**Procedure**
- 1. From the bash, create a new directory for your Docker image, how to exemple:
```
mkdir /home/dockerDB2
```

- 2. Go to this directory by entering the following command:
```
cd /home/dockerDB2
```

> **Note** Docker uses a configuration file, config.json, for unencrypted storage of credentials. As a result, prior to entering your user name and password, you will receive the message, WARNING: Error loading config file...., followed by the expected default location of the config.json file.
This message will not prevent you from entering your credentials and accessing your Docker environment. Once you have logged into Docker creates a config.json file and stores your credentials in the file at the default location. See docker login for information on creating secure storage of your Docker credentials.

- 3. Log into your Docker container:
```
docker login
```

- 4. Pull the Db2 Docker image from Docker Hub:
```
docker pull ibmcom/db2
```

- 5. From your Docker folder, create an environment variables file, .env_list, for your Db2 Community Edition image:
```
touch .env_list
```

Be sure to include the quotation symbols when creating the file.
- 6. In a text editor, open the .env_list file and paste the following:

```
LICENSE=accept
DB2INSTANCE=db2inst1
DB2INST1_PASSWORD=<yourpasswd>
DBNAME=testdb
BLU=false
ENABLE_ORACLE_COMPATIBILITY=false
UPDATEAVAIL=NO
TO_CREATE_SAMPLEDB=true
REPODB=false
IS_OSXFS=true
PERSISTENT_HOME=false
HADR_ENABLED=false
ETCD_ENDPOINT=
ETCD_USERNAME=
ETCD_PASSWORD=
```

- 8. Enter and run the following command to enter the Docker container:
```
docker run -h mydb2 --name mydb2  --restart=always --detach --privileged=true -p 50000:50000 -p 55000:55000 --env-file .env_list -v /home/dockerDB2:/database ibmcom/db2
```

### 3. Connecting DB2 on Docker with DBeaver
After installation DB2 Docker, we will connect DB2 to the DBeaver database tool.
> You need to create a connection in DBeaver on DB2 based, you can find out how to do this by <a href="https://github.com/ca-cwds/intake/wiki/Install-DBeaver-and-Connect-to-PreInt-DB2" target="_blank">clicking here</a> *(Last Access: 2020-03-15)*.
Here you will need change only host for the IP Address that we configuration in the Ubuntu. See the Image Below

*Host with IP ADDRESS*
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/3.0.0.png" class="center">

*Test connection*
<img src="https://github.com/weslen02/connect-db2-via-dbeaver-to-docker-on-ubuntu-vm-hyper-v/blob/master/img/3.0.1.png" class="center">

### 4. Reference
Last access 2020-02-16.
- [IBM Install Docker](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.5.0/com.ibm.db2.luw.qb.server.doc/doc/t_install_db2CE_win_img.html?view=embed)

- [Run Ubuntu virtual machines made even easier with Hyper-V Quick Create](https://blogs.windows.com/windowsdeveloper/2018/09/17/run-ubuntu-virtual-machines-made-even-easier-with-hyper-v-quick-create/)

- [Install DBeaver and Connect to PreInt DB2](https://github.com/ca-cwds/intake/wiki/Install-DBeaver-and-Connect-to-PreInt-DB2)

- [Docker DB2](https://hub.docker.com/r/ibmcom/db2)

### 5. About
This is not a reference document, but it aims to share knowledge, you can help improve it, I know that the english applied here is not the best, I'm brazilian and I'm learning this new language, so if you find mistakes, I apologize, and also I ask you to do a Fork and help me to improve this document so that other people can better understand it and so maybe solve a blocker.

> **Together**, *we can* do more through the IT!

<img src="https://github.com/weslen02/end-img/blob/master/img/tks.png" class="center">

by:

<img src="https://github.com/weslen02/end-img/blob/master/assWeslen2.png" class="center">


> A good **knowledge** is **shared knowledge**!
