# Apache Spark | Troubleshooting Spark performance issues

## Scenario: 

## Pre-reqs :
  Download spark-events for the application that you are troubleshooting from the source spark history UI. 
  Copy the Loading spark events from a different cluster to spark-events folder. Next start spark history server from /<spark-installation=folder>/sbin/start-history-server.sh.
  
```
sudo /opt/spark/spark-2.4.5-bin-hadoop2.7/sbin/start-history-server.sh
starting org.apache.spark.deploy.history.HistoryServer, logging to /opt/spark/spark-2.4.5-bin-hadoop2.7/logs/spark-root-org.apache.spark.deploy.history.HistoryServer-1-kcubuntu.out
```

  Browse to spark history UI to see the event for Application copied from a different machine loaded.
  
