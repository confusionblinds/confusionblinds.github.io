---
Apache Spark | Issues observed when downloading and starting up of Spark
description: Learn how to resolve an IllegalArgumentException when running Apache Spark jobs using Azure Data Factory.
services: apache spark
author: csunilkumar
---
# Apache Spark | Issues observed when downloading and starting up of Spark

## Scenario: Downloaded Spark binary without hadoop from  [spark-2.4.5-bin-without-hadoop.tgz](https://downloads.apache.org/spark/spark-2.4.5/spark-2.4.5-bin-without-hadoop.tgz and run spark-shell to fail with following error

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

## Cause
Once downloaded, follow this article [use Hadoop’s ‘classpath’ command](https://spark.apache.org/docs/latest/hadoop-provided.html) to tell spark where to find hadoops classpath.  
Steps.
-	Find ```spark-env.sh.template``` under conf folder, copyspark-env.sh.template to spark-env.sh.  
-	Edit spark-env.sh with this at the very end.
``` export SPARK_DIST_CLASSPATH=$(/usr/local/hadoop/bin/hadoop classpath) ```  
-	Change " the/usr/local/hadoop ..." to whereever hadoop is installed
-	You can test if the classpath is produced by hadoop by simply typing in the command:```/usr/local/hadoop/bin/hadoop classpath```
- 	Should return something like ```/usr/local/hadoop/etc/hadoop:/usr/local/hadoop/share/hadoop/common/lib/*:/usr/local/hadoop/share/hadoop/common/*:/usr/local/hadoop/share/hadoop/hdfs:/usr/local/hadoop/share/hadoop/hdfs/lib/*:/usr/local/hadoop/share/hadoop/hdfs/*:/usr/local/hadoop/share/hadoop/yarn/lib/*:/usr/local/hadoop/share/hadoop/yarn/*:/usr/local/hadoop/share/hadoop/mapreduce/lib/*:/usr/local/hadoop/share/hadoop/mapreduce/*:/usr/local/hadoop/contrib/capacity-scheduler/*.jar```

## Conclusion

Adding ```export SPARK_DIST_CLASSPATH=$(/usr/local/hadoop/bin/hadoop classpath)``` at the end of the spark-env.sh  will work to glue spark to hadoop.
