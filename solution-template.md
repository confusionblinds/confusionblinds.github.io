---
title: Azure HDInsight Solutions | Spark | Unable to start Zeppelin service on a HDInsight spark cluster
description: Learn how to resolve Zeppelin startup failures
services: hdinsight
author: csunilkumar
ms.author: sunilkc
ms.service: hdinsight
ms.custom: troubleshooting
ms.topic: conceptual
ms.date: 10/22/2019
---

# Azure HDInsight Solutions | Zeppelin | Unable to start Zeppelin service on a HDInsight spark cluster

## Issue:  Unable to start Zeppelin service from Ambari UI, part of the error would the following path does not exist.

```
"/usr/hdp/current/zeppelin-server/bin/zeppelin-daemon.sh: No such file or directory"
```

```
Could not determine stack version for component zeppelin-server by calling '/usr/bin/hdp-select status zeppelin-server > /tmp/tmpijeBJ9'. Return Code: 1, Output: .
2019-09-27 11:16:01,800 - The 'zeppelin-server' component did not advertise a version. This may indicate a problem with the component packaging. However, the stack-select tool was able to report a single version installed (2.6.5.3008-11). This is the version that will be reported.
```

## Cause

 Identified the symbol link "/usr/hdp/current/zeppelin-server" was missing on headnode0.

## Solution

 We created the symbolic link on headnode0 by following the headnode1 where symlink looked fine.
 ```
 sudo ln -s  /usr/hdp/3.1.2.1-1/zeppelin /usr/hdp/current/zeppelin-server
 ```
