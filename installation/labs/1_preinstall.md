#Pre-installation process
* Update system
```[root@ip-172-31-34-127 ~]# yum update
```
* Check vm.swappiness.
```[root@ip-172-31-34-127 ~]#vi /etc/sysctl.conf
vm.swappiness = 1
- Reboot instances.
[root@ip-172-31-34-127 ~]#cat /proc/sys/vm/swappiness
1
```

