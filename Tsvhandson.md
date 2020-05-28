```
wget https://datasets.imdbws.com/title.basics.tsv.g -P /home/username/Downloads/
gunzip title.basics.tsv.gz
wc -l title.basics.tsv  
6834112 title.basics.tsv

head -10  title.basics.tsv 
 tconst	titleType	primaryTitle	originalTitle	isAdult	startYear	endYear	runtimeMinutes	genres
tt0000001	short	Carmencita	Carmencita	0	1894	\N	1Documentary,Short
tt0000002	short	Le clown et ses chiens	Le clown et ses chiens	0	1892	\N	5	Animation,Short
tt0000003	short	Pauvre Pierrot	Pauvre Pierrot	0	1892	\N	4Animation,Comedy,Romance
tt0000004	short	Un bon bock	Un bon bock	0	1892	\N	12	Animation,Short
tt0000005	short	Blacksmith Scene	Blacksmith Scene	0	1893	\N	1	Comedy,Short
tt0000006	short	Chinese Opium Den	Chinese Opium Den	0	1894	\N	1	Short
tt0000007	short	Corbett and Courtney Before the Kinetograph	Corbett and Courtney Before the Kinetograph	0	1894	\N	1	Short,Sport
tt0000008	short	Edison Kinetoscopic Record of a Sneeze	Edison Kinetoscopic Record of a Sneeze	0	1894	\N	1	Documentary,Short
tt0000009	movie	Miss Jerry	Miss Jerry	0	1894	\N	45	Romance
```

```
val titlesRDD = spark.read.format("csv").option("sep","\t").option("header","true").option("inferSchema","true").load("/home/sunil/Downloads/title.basics.tsv").rdd

titlesRDD.take(10)'

Number of line entries in the file

val totalRecords = titlesRDD.count()
println(s"Number of records in the data file: $totalRecords")
```

How many types of Titles are store in the titles file?
```
println(s"Q1: How many types of Titles are store in the titles file?")
val titleOnlyTypeRDD = titlesRDD.map(x => x(1))
distinctTitleTypeRDD.distinct().collect().foreach(println)
```

// Q2: How many Titles of each type of category?
```
println(s"Q2: How many Titles for each type of category?")

val distinctTypesOfCallsSortedRDD = TitleOnlyTypeRDD.map(x => (x, 1)).reduceByKey((x, y) => (x + y)).map(x => (x._2, x._1)).sortByKey(false)
distinctTypesOfCallsSortedRDD.collect().foreach(println)
```

val titlesRDD = spark.read.format("csv").option("sep","\t").option("header","true").option("inferSchema","true").load("/home/sunil/Downloads/title.basics.tsv").rdd


scala> val titleOnlyTypeRDD = titlesRDD.map(x => x(1))
titleOnlyTypeRDD: org.apache.spark.rdd.RDD[Any] = MapPartitionsRDD[23] at map at <console>:25

scala>  titleOnlyTypeRDD.take(10)
res10: Array[Any] = Array(short, short, short, short, short, short, short, short, movie, short)

scala> val eachTitleMappedRDD = titleOnlyTypeRDD.map(x => (x, 1))
eachTitleMappedRDD: org.apache.spark.rdd.RDD[(Any, Int)] = MapPartitionsRDD[24] at map at <console>:25

scala> eachTitleMappedRDD.take(10)
res11: Array[(Any, Int)] = Array((short,1), (short,1), (short,1), (short,1), (short,1), (short,1), (short,1), (short,1), (movie,1), (short,1))

scala> val titleCountRDD = eachTitleMappedRDD.reduceByKey((x, y) => (x + y))
titleCountRDD: org.apache.spark.rdd.RDD[(Any, Int)] = ShuffledRDD[25] at reduceByKey at <console>:25

scala> titleCountRDD.collect().foreach(println)
(video,265838)
(short,741249)
(tvSpecial,29202)
(tvSeries,184519)
(tvEpisode,4871527)
(tvMovie,121206)
(videoGame,25559)
(tvShort,12557)
(tvMiniSeries,31099)
(movie,551355)


scala> titleCountRDD
   val titleCountRDD: org.apache.spark.rdd.RDD[(Any, Int)]


// Return second element of tuple first and then First element which is nothing swaping.
scala> val resultRDD = titleCountRDD.map(x => (x._2, x._1))

scala>  resultRDD.collect().foreach(println)

(265838,video)                                                                  
(741249,short)
(29202,tvSpecial)
(184519,tvSeries)
(4871527,tvEpisode)
(121206,tvMovie)
(25559,videoGame)
(12557,tvShort)
(31099,tvMiniSeries)
(551355,movie)


val titlePerCategoryRDD =  resultRDD.sortByKey(true)
titlePerCategoryRDD: org.apache.spark.rdd.RDD[(Int, Any)] = ShuffledRDD[25] at sortByKey at <console>:25

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





we are adding a new column with value 1 for each word, the result of the RDD is PairRDDFunctions which contains key-value pairs, word of type String as Key and 1 of type Int as value.


// Q3: HOW MANY YEARS OF FIRE SERVICE CALLS IS IN THE DATA FILES AND INCIDENTS PER YEAR?
println(s"Q3: HOW MANY YEARS OF FIRE SERVICE CALLS IS IN THE DATA FILES AND INCIDENTS PER YEAR?")
 val fireServiceCallYearsRDD = filteredFireServiceCallRDD.map(convertToYear).map(x => (x, 1)).reduceByKey((x, y) => (x + y)).map(x => (x._2, x._1)).sortByKey(false)
fireServiceCallYearsRDD.take(20).foreach(println)
// Q4: HOW MANY SERVICE CALLS WERE LOGGED IN FOR THE PAST 7 DAYS?
println(s"Q4: HOW MANY SERVICE CALLS WERE LOGGED IN FOR THE PAST 7 DAYS?")
val last7DaysServiceCallRDD = filteredFireServiceCallRDD.map(convertToDate).map(x => (x, 1)).reduceByKey((x, y) => (x + y)).sortByKey(false)
last7DaysServiceCallRDD.take(7).foreach(println)
// Q5: WHICH NEIGHBORHOOD IN SF GENERATED THE MOST CALLS LAST YEAR? 
println(s"Q5: WHICH NEIGHBORHOOD IN SF GENERATED THE MOST CALLS LAST YEAR?")
val neighborhoodDistrictCallsRDD = filteredFireServiceCallRDD.filter(row => (convertToYear(row) == "2016")).map(x => x(31)).map(x => (x, 1)).reduceByKey((x, y) => (x + y)).map(x => (x._2, x._1)).sortByKey(false)
neighborhoodDistrictCallsRDD.collect().foreach(println)





