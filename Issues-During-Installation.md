---
Apache Spark | Issues observed when downloading and starting up of Spark
description: Learn how to resolve an IllegalArgumentException when running Apache Spark jobs using Azure Data Factory.
services: apache spark
author: csunilkumar
---
# Apache Spark | Issues observed when downloading and starting up of Spark

## Scenario: Downloaded Spark binary without hadoop from  [spark-2.4.5-bin-without-hadoop.tgz](https://downloads.apache.org/spark/spark-2.4.5/spark-2.4.5-bin-without-hadoop.tgz)

```root@kcubuntu:/opt/spark/spark-2.4.5-bin-without-hadoop# ./bin/spark-shell
/opt/spark/spark-2.4.5-bin-without-hadoop/conf/spark-env.sh: line 70: /usr/hadoop/hadoop-3.2.1/bin/hadoop: No such file or directory
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main" java.lang.NoClassDefFoundError: org/slf4j/Logger
	at java.lang.Class.getDeclaredMethods0(Native Method)
	at java.lang.Class.privateGetDeclaredMethods(Class.java:2701)
	at java.lang.Class.privateGetMethodRecursive(Class.java:3048)
	at java.lang.Class.getMethod0(Class.java:3018)
	at java.lang.Class.getMethod(Class.java:1784)
	at sun.launcher.LauncherHelper.validateMainClass(LauncherHelper.java:650)
	at sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java:632)
Caused by: java.lang.ClassNotFoundException: org.slf4j.Logger
	at java.net.URLClassLoader.findClass(URLClassLoader.java:382)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:418)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:352)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:351)
	... 7 more


```

## Issue

You receive the following exception when trying to execute a Spark activity in an Azure Data Factory pipeline:

```java
Exception in thread "main" java.lang.IllegalArgumentException: 
Wrong FS: wasbs://additional@xxx.blob.core.windows.net/spark-examples_2.11-2.1.0.jar, expected: wasbs://wasbsrepro-2017-11-07t00-59-42-722z@xxx.blob.core.windows.net
```

## Cause

A Spark job will fail if the application jar file is not located in the Spark cluster’s default/primary storage.

This is a known issue with the Spark open source framework tracked in this bug: [Spark job fails if fs.defaultFS and application jar are different url](https://issues.apache.org/jira/browse/SPARK-22587)

This issue has been resolved in Spark 2.3.0

## Solution

Make sure the application jar is stored on the default/primary storage for the HDInsight cluster. In case of Azure Data Factory make sure the ADF linked service is pointed to the HDInsight default container rather than a secondary container.
