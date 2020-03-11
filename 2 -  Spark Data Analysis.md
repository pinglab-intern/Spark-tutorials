# Functional Programming

Spark is written in a functional programming language like Scala. PySpark API is used in Spark. 
<p></p>
Example:
<br>
MapReduce problem, where we count unmber of times a song is played. The code went through each record with name of song and numbr 1. This tuple was shuffled and reduced to sum up one's in the values. This was a functional approach to counting the songs. In preocedural programming, we'd use a counter to keep track of each song, iterate through all the songs, and incerement the counter by 1 if the song name matched. 

# Why functional programming?

Good for distributed systems. Distributed system is a bunch of maciens working together. Functional programming helps minimize mistakes that can cripple a distributed programming system.  

# Song example in Spark

In parallel programming, sparks splits up data onto multiple machines. If songs were splot into 2 machines, machine A would need to finish its counting before retunrning result to MAchine B so hat B could add to the count. In Spark actually, MAchine A counts the number of times Despacit appears, and machine B does the same and then they combine their results. 

# Pure Functions analogy

Program is a bread factory, function is a specific machine in the factory that makes sourdough bread.If we make bread, we can cut some corners as long as general recipe is followed. If it needs mass production, the brea dmakers need to be consistent wihtout side effects. The machine needs to leave the factory in same condition before it ran. Example, one machine increases tempreature, then all machines increase temperature. 
<p></p>
In distributed systems, function shouldnt have side ffects with variables outside scope. Another issue is contamination of original ingredients. Mother dough makes copies of the starter. In systems, when a function runs on input data, it can't alter it in the process. If the functions preserve inputs and avoid side effects, these are pure functions. 

# Spark DAGs


Every spark function makes a copy of unput data. The parent data is immutable. When there are many functions, you chain multiple functions that each accompish a small pat of work. A function also has multiple subfunctions. Each subfcuntion ahs to be pure along with master function. 
<br>
Lazy Evaluatoon = First builds steps for what functions and data will be need. This is called the Directed Acylic Graph. Grab all the ingredients in one step. In Spark, multistep combos are calle dstages.

# Maps and Lambda

Maps make a copy of original input data and transform the opy into whatever function you put inside the map. After some initialization we convert the songs into a distributed dataset. This used sc (Spark contest) object and ahs a method parallelize that takes an object and dstirbutes it across cluster. One step is to make the song title lower case.  
<p></p>
Then we use map to apply our function to each song in the dataset. The Spark commands use lazy eval (songs aren't converted yet). Spark waits until last minute to combine steps into a single stage. T take action, collect function gatehrs results from all machines in cluster back to machine running th enotebok. The origial song long is still intact. 
<p></p>
Lambda function (anonymous functions). USe lambda, then write input of function followed by colona nd expected output.Left is input definition, and rightside is the output. You can just define functions if preferred.  

# Loading Data

HTML: Scrape data from internet uses HTML.
<br>
XML: A generakized ersion of HTML where tags don't have specific meaning.

# Distributed Data Stores

Distributed file systems store data ina fault tolerant waym, so if machine cant be used information isnt lsot. Hadoop has HDFS. Itsplits fils into 64 or 128 mbs, and replicates them across the cluster. We can use AWS simple storage service. Companies often use S3 to store raw data collected

# SparkSession

Spark prgrams have sparkcontext: connects cluster with the application. We need SparkConf object to secify some info abut the web applicatoin like its name. We can also put "local" as master. 

To read dataframes, we use SparkSession, where we specify paramteres to create a Spark session. getOrCreate() returns old Spark session and paraeters will be defined to new configurations instead of starting a new Session.

# Reading and writing Data into Spark

`from pyspark.sql import SparkSession`
`u`

# Imperative vs Declarative 

Imperative programming: concerned with how
Declarative: cares about the what
<p></p>
Declarative:let's get a cake for Julia. more concerned about result
Imperative: Steps to get the cak for Julia. more concerned with how to get the result

# Wrangling Data Frames

Read into user log data frame
`user_log = spark.read.json(path)`
<br>
Print schema:
<br>
`user_log.printSchema()`
<br>
`user_log.describe().show()` shows some summary statistics
<br>
`user_log.describe('artist').show()`
<br>
`user_log.count()` checks how many rows we have in data.frame
<br>
`user_log.select('page').dropDuplicates().sort("page").show()` sorts these different options alphabetically
<br>
`user_log.select(["userId", "firstname", "page", "song"]).where(user_log.userId == "1046").collect()`
<br>
`user_log = user_log.withColumn("hour", get_hour(user_log.ts))` event log of songs
<br> 
`get_hour = udf(lambda x: datetime.datetime.fromtimestamp(x / 1000.0). hour)` user defined function (udf) called `get_hour` to get hour of the day, and we add it as a new column
<br>
<br>
`user_log = user_log.withColumn("hour", get_hour(user_log.ts))  `