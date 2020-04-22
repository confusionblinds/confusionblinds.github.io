# Apache Spark | Download spark, create a local setup.

## Scenario: Learn how to download, setup up spark binary that are ready to execute sample locally on a linux machine.

## Pre-reqs
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

