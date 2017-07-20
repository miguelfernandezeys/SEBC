# Storage lab
* **Create end-user Linux account in all nodes.**

```
sudo groupadd miguel
sudo useradd -g miguel miguel
sudo passwd miguel
password miguel
```
* **Registered users at each node.**
```
more /etc/passwd
sentry:x:980:976:Sentry:/var/lib/sentry:/sbin/nologin
impala:x:979:975:Impala:/var/lib/impala:/bin/bash
spark:x:978:974:Spark:/var/lib/spark:/sbin/nologin
hue:x:977:973:Hue:/usr/lib/hue:/bin/false
miguel:x:1001:1001::/home/miguel:/bin/bash
```
* **HDFS directory**
```
sudo -u hdfs hdfs dfs -mkdir /user/miguel
sudo -u hdfs hdfs dfs -chown -R miguel:miguel /user/miguel
sudo -u hdfs hdfs dfs -ls /user
```
*Output created directory*
```
drwxr-xr-x   - miguel   miguel            0 2017-07-18 19:04 /user/
```
* **Teragen job** 
```
cd CDH/lib/hadoop-0.20-mapreduce/ CDH-5.11.1-1.cdh5.11.1.p0.4/jars/
hadoop jar hadoop-mapreduce-examples-2.6.0-cdh5.11.1.jar teragen -Ddfs.blocksize=32M -Dmapred.map.tasks=4 100000000 /user/miguel/output
```
*Output*
```
hdfs dfs -ls /user/miguel/output
Found 5 items
-rw-r--r--   3 miguel miguel          0 2017-07-18 19:36 /user/miguel/output/_SUCCESS
-rw-r--r--   3 miguel miguel 2500000000 2017-07-18 19:36 /user/miguel/output/part-m-00000
-rw-r--r--   3 miguel miguel 2500000000 2017-07-18 19:36 /user/miguel/output/part-m-00001
-rw-r--r--   3 miguel miguel 2500000000 2017-07-18 19:36 /user/miguel/output/part-m-00002
-rw-r--r--   3 miguel miguel 2500000000 2017-07-18 19:36 /user/miguel/output/part-m-00003
```
* **Time teragen**
```
real    2m4.561s
user    0m5.432s
sys     0m0.298s
```

* **Terasort**
```
hadoop jar hadoop-mapreduce-examples-2.6.0-cdh5.11.1.jar terasort -Ddfs.blocksize=32M -Dmapred.map.tasks=4  /user/miguel/output /user/miguel/output2
time terasort
time hadoop jar hadoop-mapreduce-examples-2.6.0-cdh5.11.1.jar terasort -Ddfs.blocksize=32M -Dmapred.map.tasks=4  /user/miguel/output /user/miguel/output2
````

* **Time terasort**

```
real    7m1.920s
user    0m8.093s
sys     0m0.467s
```


