# Snapshots lab
* **Download master.zip**

wget https://github.com/miguelfernandezeys/SEBC/archive/master.zip

* **Directory precious**

sudo -u hdfs hdfs dfs -mkdir /user/precious

* **Copy master.zip to precious directory

sudo -u hdfs hdfs dfs -copyFromLocal /var/master.zip /user/precious
sudo -u hdfs hdfs dfs -ls /user/precious

*Output 

Found 1 items
-rw-r--r--   3 hdfs neosagan     474826 2017-07-18 19:50 /user/neosagan/precious/SEBC-master.zip

* **Enable snapshot

 hdfs dfsadmin -allowSnapshot /user/precious
 
* **Create snapshot

sudo -u hdfs hdfs dfs -createSnapshot /user/precious copia
sudo -u hdfs hdfs dfs -ls /user/precious/.snapshot

*Output

Created snapshot /user/precious/.snapshot/copia

* **Drop master.zip

sudo -u hdfs hdfs dfs -rm -R /user/precious/master.zip

*Output

17/07/18 20:12:17 INFO fs.TrashPolicyDefault: Moved: 'hdfs://ip-172-31-37-35.us-west-2.compute.internal:8020/user/precious/master.zip' to trash at: hdfs://ip-172-31-37-35.us-west-2.compute.internal:8020/user/hdfs/.Trash/Current/user/precious/master.zip

*¨**Restore deleted file

sudo -u hdfs hdfs dfs -cp /user/precious/.snapshot/copia/master.zip /user/precious


