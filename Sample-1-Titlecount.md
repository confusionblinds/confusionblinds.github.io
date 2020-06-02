scala> val titlesRDD = spark.read.format("csv").option("sep","\t").option("header","true").option("inferSchema","true").load("/home/sunil/Downloads/title.basics.tsv").rdd
titlesRDD: org.apache.spark.rdd.RDD[org.apache.spark.sql.Row] = MapPartitionsRDD[14] at rdd at <console>:23

scala> val titleOnlyTypeRDD = titlesRDD.map(x => x(1))
titleOnlyTypeRDD: org.apache.spark.rdd.RDD[Any] = MapPartitionsRDD[15] at map at <console>:25

scala> val eachTitleMappedRDD = titleOnlyTypeRDD.map(x => (x, 1))
eachTitleMappedRDD: org.apache.spark.rdd.RDD[(Any, Int)] = MapPartitionsRDD[16] at map at <console>:25

scala> val titleCountRDD = eachTitleMappedRDD.reduceByKey((x, y) => (x + y))
titleCountRDD: org.apache.spark.rdd.RDD[(Any, Int)] = ShuffledRDD[17] at reduceByKey at <console>:25

scala> val resultRDD = titleCountRDD.map(x => (x._2, x._1))
resultRDD: org.apache.spark.rdd.RDD[(Int, Any)] = MapPartitionsRDD[18] at map at <console>:25

scala> val titlePerCategoryRDD =  resultRDD.sortByKey(true)
titlePerCategoryRDD: org.apache.spark.rdd.RDD[(Int, Any)] = ShuffledRDD[21] at sortByKey at <console>:25

scala> titlePerCategoryRDD.collect().foreach(println)
(12557,tvShort)
(25559,videoGame)
(29202,tvSpecial)
(31099,tvMiniSeries)
(121206,tvMovie)
(184519,tvSeries)
(265838,video)
(551355,movie)
(741249,short)
(4871527,tvEpisode)
