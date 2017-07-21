* **Teragen command**
```
time hadoop jar /opt/cloudera/parcels/CDH-5.11.1-1.cdh5.11.1.p0.4/jars/hadoop-mapreduce-examples-2.6.0-cdh5.11.1.jar teragen -Dmapreduce.job.maps=8 -Dmapreduce.map.memory.mb=32 -Dmapreduce.map.java.opts.max.heap=512 65536000 /user/saturn/tgen

```
-> Output
```
real    1m3.846s
user    0m5.425s
sys     0m0.254s

```
* **Output -ls hdfs dfs -ls /user/saturn/tgen**
 hdfs dfs -ls /user/saturn/tgen
Found 9 items
-rw-r--r--   3 haley haley          0 2017-07-21 18:30 /user/saturn/tgen/_SUCCESS
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00000
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00001
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00002
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00003
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00004
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00005
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00006
-rw-r--r--   3 haley haley  819200000 2017-07-21 18:30 /user/saturn/tgen/part-m-00007

* **Output hadoop fsck -blocks /user/saturn*
```
[haley@ip-172-31-44-71 centos]$ hadoop fsck -blocks /user/saturn
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://ip-172-31-44-71.us-west-2.compute.internal:50070
FSCK started by haley (auth:SIMPLE) from /172.31.44.71 for path /user/saturn at Fri Jul 21 18:34:10 UTC 2017
.........Status: HEALTHY
 Total size:    6553600000 B
 Total dirs:    2
 Total files:   9
 Total symlinks:                0
 Total blocks (validated):      56 (avg. block size 117028571 B)
 Minimally replicated blocks:   56 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Fri Jul 21 18:34:10 UTC 2017 in 5 milliseconds
```
