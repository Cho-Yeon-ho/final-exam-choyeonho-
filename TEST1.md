# 1. Create a CDH Cluster on AWS

## a.
### 1. Add the following linux accounts to all nodes
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

[centos@mn ~]$ sudo -i
[root@mn ~]# useradd training -u 3800
[root@mn ~]# passwd training
Changing password for user training.
New password:
BAD PASSWORD: The password contains the user name in some form
Retype new password:
passwd: all authentication tokens updated successfully.
[root@mn ~]# groupadd skcc
[root@mn ~]# gpasswd -a training skcc
Adding user training to group skcc
[root@mn ~]# vi /etc/sudoers



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

/etc/centos-release:CentOS Linux release 7.6.1810 (Core)
/etc/os-release:NAME="CentOS Linux"
/etc/os-release:VERSION="7 (Core)"
/etc/os-release:ID="centos"
/etc/os-release:ID_LIKE="rhel fedora"
/etc/os-release:VERSION_ID="7"
/etc/os-release:PRETTY_NAME="CentOS Linux 7 (Core)"
/etc/os-release:ANSI_COLOR="0;31"
/etc/os-release:CPE_NAME="cpe:/o:centos:centos:7"
/etc/os-release:HOME_URL="https://www.centos.org/"
/etc/os-release:BUG_REPORT_URL="https://bugs.centos.org/"
/etc/os-release:CENTOS_MANTISBT_PROJECT="CentOS-7"
/etc/os-release:CENTOS_MANTISBT_PROJECT_VERSION="7"
/etc/os-release:REDHAT_SUPPORT_PRODUCT="centos"
/etc/os-release:REDHAT_SUPPORT_PRODUCT_VERSION="7"
/etc/redhat-release:CentOS Linux release 7.6.1810 (Core)
/etc/system-release:CentOS Linux release 7.6.1810 (Core)


### 4. List the file system capacity for the first node (master node)
df -h

[root@mn ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p1  100G  1.3G   99G   2% /
devtmpfs        7.6G     0  7.6G   0% /dev
tmpfs           7.6G     0  7.6G   0% /dev/shm
tmpfs           7.6G   17M  7.6G   1% /run
tmpfs           7.6G     0  7.6G   0% /sys/fs/cgroup
tmpfs           1.6G     0  1.6G   0% /run/user/0
tmpfs           1.6G     0  1.6G   0% /run/user/1000



### 5. List the command and output for yum repolist enabled
yum repolist enabled

[root@mn ~]# yum repolist enabled
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: ftp.neowiz.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
repo id                             repo name                             status
!base/7/x86_64                      CentOS-7 - Base                       10,019
!extras/7/x86_64                    CentOS-7 - Extras                        409
!updates/7/x86_64                   CentOS-7 - Updates                     2,076
repolist: 12,504



### 6. List the /etc/passwd entries for training (only in master name node)
sudo vi /etc/passwd 

root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
chrony:x:998:995::/var/lib/chrony:/sbin/nologin
centos:x:1000:1000:Cloud User:/home/centos:/bin/bash
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
ntp:x:38:38::/etc/ntp:/sbin/nologin
training:x:3800:3800::/home/training:/bin/bash




### 7. List the /etc/group entries for skcc (only in master name node)
sudo vi /etc/group

root:x:0:
bin:x:1:
daemon:x:2:
sys:x:3:
adm:x:4:centos
tty:x:5:
disk:x:6:
lp:x:7:
mem:x:8:
kmem:x:9:
wheel:x:10:centos
cdrom:x:11:
mail:x:12:postfix
man:x:15:
dialout:x:18:
floppy:x:19:
games:x:20:
tape:x:33:
video:x:39:
ftp:x:50:
lock:x:54:
audio:x:63:
nobody:x:99:
users:x:100:
utmp:x:22:
utempter:x:35:
input:x:999:
systemd-journal:x:190:centos
systemd-network:x:192:
dbus:x:81:
polkitd:x:998:
rpc:x:32:
ssh_keys:x:997:
cgred:x:996:
rpcuser:x:29:
nfsnobody:x:65534:
sshd:x:74:
postdrop:x:90:
postfix:x:89:
chrony:x:995:
centos:x:1000:
nscd:x:28:
ntp:x:38:
training:x:3800:
skcc:x:3801:training



### 8. List output of the following commands:
1) getent group skcc

[root@cm ~]# getent group skcc
skcc:x:3801:training


2) getent passwd training

[root@cm ~]# getent passwd training
training:x:3800:3800::/home/training:/bin/bash


