# Pre-installation process
* **Update system.**
```
[root@ip-172-31-47-166 ~]# yum update
```
* **Selinux disabled.**
```
[root@ip-172-31-47-166 ~]#sudo nano /etc/selinux/config
selinux =disabled
```
 -> Reboot instances and verify sestatus.
```
[centos@ip-172-31-47-166 ~]$ sestatus
SELinux status:                 disabled
```
* **Check vm.swappiness.**
```
[root@ip-172-31-34-127 ~]#vi /etc/sysctl.conf
vm.swappiness = 1
```
 -> Reboot instances and verify swappiness.
```
[root@ip-172-31-47-166 ~]#cat /proc/sys/vm/swappiness
1
```
* **Mount volumen.**
```
sudo mkdir /data0
sudo mkfs -t ext3 /dev/xvdc 
sudo mount /dev/xvdc  /data0
df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       40G  8.6G   32G  22% /
devtmpfs        7.3G     0  7.3G   0% /dev
tmpfs           7.2G     0  7.2G   0% /dev/shm
tmpfs           7.2G   17M  7.2G   1% /run
tmpfs           7.2G     0  7.2G   0% /sys/fs/cgroup
/dev/xvdc        37G   49M   35G   1% /data0
/dev/xvdb        37G   49M   35G   1% /mnt
tmpfs           1.5G     0  1.5G   0% /run/user/995
tmpfs           1.5G     0  1.5G   0% /run/user/0
cm_processes    7.2G  2.1M  7.2G   1% /run/cloudera-scm-agent/process
tmpfs           1.5G     0  1.5G   0% /run/user/1000

echo "/dev/xvdc /data0 ext3 noatime 0 0"  | sudo tee -a /etc/fstab
```
* **Disable transparent hugepage.** 
```
echo "never" > /sys/kernel/mm/transparent_hugepage/defrag
echo "never" > /sys/kernel/mm/transparent_hugepage/enabled
vi /etc/rc.local
echo "never" > /sys/kernel/mm/transparent_hugepage/defrag
echo "never" > /sys/kernel/mm/transparent_hugepage/enabled
```
* **Network interface configuration.**
```
[centos@ip-172-31-47-166 ~]$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.47.166  netmask 255.255.240.0  broadcast 172.31.47.255
        inet6 fe80::415:bfff:fe44:8974  prefixlen 64  scopeid 0x20<link>
        ether 06:15:bf:44:89:74  txqueuelen 1000  (Ethernet)
        RX packets 594  bytes 187630 (183.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1078  bytes 84208 (82.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
* **Forward and reverse host lookups.**
```
[centos@ip-172-31-47-166 ~]$ host 172.31.47.166
[centos@ip-172-31-47-166 ~]$ 166.47.31.172.in-addr.arpa domain name pointer ip-172-31-47-166.us-west-2.compute.internal.
[centos@ip-172-31-47-166 ~]$ getent ahosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
172.31.47.166   ip-172-31-47-166.us-west-2.compute.internal
172.31.37.35    ip-172-31-37-35.us-west-2.compute.internal
172.31.39.66    ip-172-31-39-66.us-west-2.compute.internal
172.31.32.37    ip-172-31-32-37.us-west-2.compute.internal
172.31.37.171   ip-172-31-37-171.us-west-2.compute.internal
```
* **Nscd status.**
```
[centos@ip-172-31-47-166 ~]$ sudo systemctl status nscd
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2017-07-20 17:50:04 UTC; 4s ago
  Process: 12871 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 12872 (nscd)
   CGroup: /system.slice/nscd.service
           └─12872 /usr/sbin/nscd

Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal nscd[12872]: 1287...
Jul 20 17:50:04 ip-172-31-47-166.us-west-2.compute.internal systemd[1]: Start...
Hint: Some lines were ellipsized, use -l to show in full.
```
* **Ntp status.**
```
[centos@ip-172-31-47-166 ~]$ sudo systemctl status ntpd
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2017-07-20 17:52:55 UTC; 5s ago
  Process: 13259 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 13260 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─13260 /usr/sbin/ntpd -u ntp:ntp -g

Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: List...
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: 0.0....
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: 0.0....
Jul 20 17:52:55 ip-172-31-47-166.us-west-2.compute.internal ntpd[13260]: 0.0....
Hint: Some lines were ellipsized, use -l to show in full.
```
* **Install MariaDB.**
```
[centos@ip-172-31-47-166 ~]$ sudo vi /etc/yum.repos.d/MariaDB.repo
# MariaDB 10.0 RedHat repository list - created 2017-07-18 16:15 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.0/rhel7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
 -> Update repos.
```
[centos@ip-172-31-47-166 ~]$ yum repolist
```
 -> Install MariaDB-server and MariaDB-client.
```
[centos@ip-172-31-47-166 ~]$ sudo yum install MariaDB-server MariaDB-client
```
 -> Enable and Start MariaDB.
```
[centos@ip-172-31-47-166 ~]$ sudo systemctl enable mysql
[centos@ip-172-31-47-166 ~]$sudo systemctl start mysql
```
 -> Execute MariaDB setting.
```
[centos@ip-172-31-47-166 ~]$ sudo mysql_secure_installation
```
 -> Set up databases.
```
create database scm DEFAULT CHARACTER SET utf8;
create user 'scm'@'localhost' IDENTIFIED BY 'scm';
grant all on scm.* TO 'scm'@'%' IDENTIFIED BY 'scm';

create database amon DEFAULT CHARACTER SET utf8;
create user 'amon'@'localhost' IDENTIFIED BY 'amon';
grant all on amon.* TO 'amon'@'%' IDENTIFIED BY 'amon';

create database rman DEFAULT CHARACTER SET utf8;
create user 'rman'@'localhost' IDENTIFIED BY 'rman';
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY 'rman';

create database metastore DEFAULT CHARACTER SET utf8;
create user 'metastore'@'localhost' IDENTIFIED BY 'metastore';
grant all on metastore.* TO 'metastore'@'%' IDENTIFIED BY 'metastore';

create database sentry DEFAULT CHARACTER SET utf8;
create user 'sentry'@'localhost' IDENTIFIED BY 'sentry';
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'sentry';

create database nav DEFAULT CHARACTER SET utf8;
create user 'nav'@'localhost' IDENTIFIED BY 'nav';
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'nav';

create database navms DEFAULT CHARACTER SET utf8;
create user 'navms'@'localhost' IDENTIFIED BY 'navms';
grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'navms';

create database hue DEFAULT CHARACTER SET utf8;
create user 'hue'@'localhost' IDENTIFIED BY 'hue';
grant all on hue.* to 'hue'@'localhost' identified by 'hue';

create database oozie;
create user 'oozie'@'localhost' IDENTIFIED BY 'oozie';
grant all privileges on oozie.* to 'oozie'@'localhost' identified by 'oozie';
grant all privileges on oozie.* to 'oozie'@'%' identified by 'oozie';

create database sqoop;
create user 'sqoop'@'localhost' IDENTIFIED BY 'sqoop';
grant all privileges on sqoop.* to 'sqoop'@'localhost' identified by 'sqoop';
grant all privileges on sqoop.* to 'sqoop'@'%' identified by 'sqoop';
```
 -> Show databases.
```MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| amon               |
| hue                |
| information_schema |
| metastore          |
| mysql              |
| nav                |
| navms              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
| sqoop              |
+--------------------+
13 rows in set (0.13 sec)
```
* **Install Java.** 

-> Server
```
[centos@ip-172-31-47-166 ~]$ sudo yum install java-1.7.0-openjdk
-Java version
[centos@ip-172-31-47-166 ~]$ java -version
java version "1.7.0_141"
OpenJDK Runtime Environment (rhel-2.6.10.1.el7_3-x86_64 u141-b02)
OpenJDK 64-Bit Server VM (build 24.141-b02, mixed mode)
```
* **JDBC** 

-> Server
```
[centos@ip-172-31-47-166 ~]$ sudo wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.42.tar.gz
[centos@ip-172-31-47-166 ~]$ tar zxvf mysql-connector-java-5.1.42.tar.gz
[centos@ip-172-31-47-166 ~]$ sudo cp mysql-connector-java-5.1.42/mysql-connector-java-5.1.42-bin.jar /usr/share/java/mysql-connector-java.jar
```
-> Agents

 *Create directory /user/share/java/*
```
 mkdir /user/share/java
 sudo cp mysql-connector-java-5.1.42/mysql-connector-java-5.1.42-bin.jar /usr/share/java/mysql-connector-java.jar
```
* **Install Cloudera manager server and agents.**
 -> Create repo Cloudera.
```
vi /etc/yum.repo.d Cloudera.repo
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64           	  
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/511.1/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera    
gpgcheck = 1
```
 -> Update repo.
```
yum repolist
```
-> Install Cloudera server - First node.
```
sudo yum install cloudera-manager-daemons cloudera-manager-server 
```
-> Install Cloudera agent - All nodes.
```
sudo yum install cloudera-manager-daemons cloudera-manager-agent
```
* **Prepare databases.**
```
[centos@ip-172-31-47-166 ~]$ cd /usr/share/cmf/schema
[centos@ip-172-31-47-166 ~]$ sudo ./scm_prepare_database.sh mysql scm scm scm  
```
* **Start cloudera-scm-server and cloudera-scm-agent.**
```
sudo service cloudera-scm-server enable
sudo service cloudera-scm-server start
sudo service cloudera-scm-server status
sudo service cloudera-scm-agent enable
sudo service cloudera-scm-agent-start
```





