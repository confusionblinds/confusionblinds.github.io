# Apache Spark | Download spark, create a local setup.

## Scenario: Learn how to download, setup up spark binary that are ready to execute sample locally on a linux machine.

## Pre-reqs
- Following steps were all followed on linux ubuntu machine.
- Make user JAVA is installed and JAVA_HOME is set right by adding ```JAVA_HOME="/opt/java/zulu-8-azure-jdk_8.46.0.19-8.0.252-linux_x64"``` at the end of the file in /etc/environment

- /etc/environment is a system-wide configuration file, which is used by all users.

## Steps
- Browse to [Apache Spark download page](http://spark.apache.org/downloads.html), select the spark prebuild with hadoop.
![Download spark](./media/download-install-local-spark-01.png)

- Download the package using wget, this will get downloaded
```
wget http://apache.mirrors.hoobly.com/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz -P /home/username/Downloads
```

- Extract the tgz to a desired location, in this case the file will be extracted to "/opt/spark"
```
sudo tar -xf spark-2.4.5-bin-hadoop2.7.tgz -C /opt/spark/
```
- Test if spark-shell gets started, browser to folder where spark binaries were extracted, ```cd /opt/spark/spark-2.4.5-bin-hadoop2.7``` and execute ```./bin/spark-shell command``` this should successfully start spark, display spark verion banner and stop at a scala prompt.

![Spark-shell](./media/download-install-local-spark-02.png)

- Launching spark web UI : In local mode spark shell runs as an application, web UI provides details about the stages, storage(cached RDDs), Environment variables and executors. Observe the Spark context Web UI URL in the image above, open a browse to key in the ip:port that you see on the command prompt. In this case it was 192.168.137.34:4040

![Spark shell application UI](./media/download-install-local-spark-03.png)




## Exploring Folders
- /bin  : 
- /conf :
- /jars :

