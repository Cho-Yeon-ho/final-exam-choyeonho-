#

# setup a password for centos
sudo passwd centos
sudo vi /etc/ssh/sshd_config
change ->
PasswordAuthentication yes
sudo systemctl restart sshd.service

# Update /etc/host
sudo vi /etc/hosts
add ->
******* THIS IS PUBLIC IP

15.164.145.67 cm.skcc.com cm
15.164.147.9 mn.skcc.com mn
15.164.35.160 dn1.skcc.com dn1
15.164.36.67 dn2.skcc.com dn2
15.164.4.140 dn3.skcc.com dn3



# 1. Create a CDH Cluster on AWS

## a.
### 1. 
1) ADD the following linux accounts to all nods
useradd training -u 3800
2) Set the password for user "training" to "training"
passwd training
3) Create the group skcc and add training to it
groupadd skcc
gpasswd -a training skcc
4) Give training sudo capabilites
vi /etc/sudoers
training ALL=(ALL) NOPASSWD: ALL


### 2. List the your instances by IP adress and DNS name ( don't use /etc/hosts for this)
sudo hostnamectl set-hostname cm.skcc.com
hostname -f
sudo hostnamectl set-hostname mn.skcc.com
hostname -f
sudo hostnamectl set-hostname dn1.skcc.com
hostname -f
sudo hostnamectl set-hostname dn2.skcc.com
hostname -f
sudo hostnamectl set-hostname dn3.skcc.com
hostname -f

### 3. List the Linux release you are using
grep . /etc/*-release

### 4. List the file system capacity for the first node (master node)
df -h

### 5. List the command and output for yum repolist enabled
yum repolist enabled

### 6. List the /etc/passwd entries for training (only in master name node)
sudo vi /etc/passwd 

### 7. List the /etc/group entries for skcc (only in master name node)
sudo vi /etc/passwd

### 8. List output of the following commands:
1) getent group skcc

2) getent passwd training
