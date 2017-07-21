* /etc/yum.repos.d
```
[centos@ip-172-31-44-71 yum.repos.d]$ ls /etc/yum.repos.d
CentOS-Base.repo  CentOS-Debuginfo.repo  CentOS-Media.repo    CentOS-Vault.repo
CentOS-CR.repo    CentOS-fasttrack.repo  CentOS-Sources.repo  Cloudera.repo
```
* Prepare script 
 ```
 sudo /usr/share/cmf/schema/scm_prepare_database.sh mysql scm scm scm  
 JAVA_HOME=/usr/lib/jvm/java-openjdk
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/lib/jvm/java-openjdk/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties  com.cloudera.cmf.db.
[main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```
