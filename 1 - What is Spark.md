# What is Big Data

When instead of using one machine,its easier to use distirbuted systems of multiple computers. 

__Numbers Everyone Should Know__

CPU: how fast to run to add 2 nos
<br>
Memory: How quickly can you look up an appt
<br>
SSD: How long does it take to load music from your SSd
<br>
Network: How much data can your computer downlaod from Netflix in a minute

# Small Data Numbers

Extraction: Filter out Canadian users, and save the artists
<br>
Split data: Email a month of data to 12 different coworkers. Each run Python program. But emailing is the slowest part of the process. And what if some people use different versions of Python? 

# Big Data Numbers

Need to make same report of most popular artists. Its not 200 GB> What happens if we use the same Python code? It goes for a few seconds, then laptop halts. 
<br>
CPU isn't a bottleneck when it comes to big data. THE CPU's job is to run small and rapid calculations. A network is generally the biggest bottleneck. The memory and storage are the bottleneck. The memory can't load data fast enough from storage, and CPU can't load memory fast enough.
<br>
Storage>memory>CPU. The program loaded nearly 8 Gigs of memory into CPU, leaving no memory for OS to run other programs.  
<br>
Email data to 40 colleagues. You get the reuslts quickly, and they email it back to you. You only have to distribute it once, and you can do this even faster by sending 2 email each of 4 gigs, and the people an process it one while the other is downloading. It takes etwork long time to send back the data, but the distribution process is fast.

# Distributed and Parallel computing

Each node has its own private memory and processor and it communicates with other nodes via messages. It is commevted to other machines in a network.
<br>
Parallel computing is a particularl tightly couple form of dsitributed computing. In paralell computing, all processors have access to a shared memory

# Hadoop

HDFS: Distributed File System
HadoopMap Reduce: MapReduce programming model
YARN: Resource Manager

# MapReduce

Analyze big file by dividing it into smaller peices, sending it to other pc's, running the processing parallel, and collecting the results. This resembles MapReduce quite closely. 
<p></p>

<p>
Example:
<br>
How many times a song was played in the last year. The log data is 100's of gigs. In the Map Reduce, we have 3 steps:
<ol>
    <li> Map </li>
    <li> Shuffle </li>
    <li> Reduce </li>
</ol>
<br>
We stored our fils in a HDFS. We first break data into chuns. These chunks are artitions. In firsts stpe, each map processor is a partition from disk transforms each record in that given partition, then rises modify records to an intermediate file. The transformation consists of 5 steps:
<br>
<ol>
<li>Read each line of log file, check if its an event describing user listening to song, check timestamp is in correct range, extract name of song, and create a tuple with the name and the number one.</li>
<li>After this, we have multple files that are key-value pairs. This data is so large, we might need multiple map rpcoessors to munch through all the data we have.</li>
<li>Shuffle: All records form intermediate files a re shuffled so that pairs with same song, the key, or key value pair end u on the same machine. This way when the node aggregates the values for a key, it can e sure it has all the corresponding data for the song and can calculate the final result.</li>
<li>In reduce, the values for a given key can be combined, and in tis case, sum all 1's for a given key. </li>
    </ol>

# Cluster

Distributed computing refers to big computational job executed across nodes. Each node is responsible for a set of operations on a subset of the data and we combine these partial results to get the final answer. How do nodes know which task to run? The master node is responsible for orchestrating the task while the workers are the ones doing the computations. 
<br>
<ul>
    <li>Local mode: We don't do distributed computing even fi we use Spark API's.</li> 
<li>Cluster amanger: Monitors availabel resources and ensures all machines are responsive during the job. There are Spark, YARN from Hadoop, and Mesos in Berkeley's Lab.</li>
<li>Spark stand alone also has a driver process. If we open a Spark shell, we are directly interacting with the driver program.</li>
    </ol>

# Spark uses

Extract and Transform data, load the data into database and then made into a dashboard using analytics tools. 