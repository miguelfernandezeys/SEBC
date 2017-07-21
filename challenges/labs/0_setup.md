# Challenge setup

* Cloud Provider 
AWS

*  Instances - IP address and DNS name
```
172.31.33.125       ip-172-31-33-125.us-west-2.compute.internal
172.31.36.134       ip-172-31-36-134.us-west-2.compute.internal
172.31.33.133      ip-172-31-33-133.us-west-2.compute.internal
172.31.42.29      ip-172-31-42-29.us-west-2.compute.internal
172.31.44.71      ip-172-31-44-71.us-west-2.compute.internal
```
* Linux release
```
cat /etc/redhat-release
CentOS Linux release 7.3.1611 (Core)
```
* File system capacity
```
 df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       30G  1.5G   29G   5% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
/dev/xvdb        37G   49M   35G   1% /mnt
tmpfs           1.5G     0  1.5G   0% /run/user/1000
tmpfs           1.5G     0  1.5G   0% /run/user/0
/dev/xvdc        37G   49M   35G   1% /data0
```
* Repos list
```
yum repolist enabled
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirrors.syringanetworks.net
 * extras: centos.den.host-engine.com
 * updates: mirror.web-ster.com
repo id                             repo name                             status
base/7/x86_64                       CentOS-7 - Base                       9,363
extras/7/x86_64                     CentOS-7 - Extras                       447
updates/7/x86_64                    CentOS-7 - Updates                    2,100
repolist: 11,910
```
* User's groups
```
sudo groupadd comets
sudo groupadd planets
```
* Users add 
```
sudo useradd -u 2800 -g comets haley
password haley
sudo useradd -u 2900 -g planets saturn
password saturn
```
* Users list
```
cat /etc/passwd
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
chrony:x:997:994::/var/lib/chrony:/sbin/nologin
centos:x:1000:1000:Cloud User:/home/centos:/bin/bash
ntp:x:38:38::/etc/ntp:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
saturn:x:2900:1002::/home/saturn:/bin/bash
haley:x:2800:1001::/home/haley:/bin/bash
```
* Group list
```
cat /etc/group
postfix:x:89:
sshd:x:74:
chrony:x:994:
centos:x:1000:
ntp:x:38:
nscd:x:28:
comets:x:1001:
planets:x:1002:
```
* Passwords list

```
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
chrony:x:997:994::/var/lib/chrony:/sbin/nologin
centos:x:1000:1000:Cloud User:/home/centos:/bin/bash
ntp:x:38:38::/etc/ntp:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
haley:x:2800:1001::/home/haley:/bin/bash
saturn:x:2900:1002::/home/saturn:/bin/bash
```

















