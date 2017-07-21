# Install a MySQL server

* Hostname of database server
 ```
 hostname
ip-172-31-33-133.us-west-2.compute.internal
```
* Available databases
```
show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| amon               |
| hue                |
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
```
* Server version
```
MariaDB [(none)]> select VERSION();
+-----------------+
| VERSION()       |
+-----------------+
| 10.0.31-MariaDB |
+-----------------+
1 row in set (0.00 sec)

```
