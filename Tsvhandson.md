

```

wget https://datasets.imdbws.com/title.basics.tsv.g -P /home/username/Downloads/

gunzip title.basics.tsv.gz

wc -l title.basics.tsv  
6834112 title.basics.tsv
```

```
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


val titlesRDD = spark.read.format("csv").option("sep","\t").option("header","true").option("inferSchema","true").load("/home/sunil/Downloads/title.basics.tsv").rdd

titlesRDD.take(10)'

val totalRecords = titlesRDD.count()
println(s"Total number of Title to be processed:$totalRecords")

How many types of titles 
val distrinctTitleType = titlesRDD.map(x => x(1))
distinctTitleType.distinct().collect().foreach(println)



distinctTitleType.distinct().collect().foreach(println)






