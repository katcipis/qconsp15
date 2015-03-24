#Intro

* Loves functional programming (Clojure) :-)
* Streaming graph is lazy evaluated, just builds graphs ([DAG](http://en.wikipedia.org/wiki/Directed_acyclic_graph) )
  with transformations and wait action to start evaluation.
* Transformations / lambda based
* Pipeline based, makes good use of cache, works on memory
* Remove synchronization requirements using function composition and algebra :D
* Core concept is a collection of functions working on arrays of data.

The presentation can be found [here](http://training.databricks.com/workshop/sparkcamp.pdf).


## MapReduce x Spark


Some ideas:

* MapReduce was made for fault tolerance (eg. disk failures on computers from 2002)
* MapReduce is made for commodity hardware from 2002
* Changes like multicores, more memory, SSD, faster networking changed the game.
* Spark tries to leverage these changes with a graph streaming model.
* MapReduce is hard to understand (hive, pig and other frameworks try to make it easier).
* Hadoop has synchronization barriers (reduce/merge phase), Spark avoids this by giving you control of checkpoints.
* Runs native Python, you have to provision the container with libraries, but it does not run on the JVM (no indirection).

I understood that Spark provides a more flexible programming model. You are not constrained
by map / reduce phases.

Since Hadoop was built on the idea of fault tolerance on a time that disk failure was high and memory was more
expensive it does a lot of heavy I/O, this leads to a poor performance when you compare hadoop with spark
(on some cases).

Later on there will be a interesting use case from spotify that relates to this idea.


## Design and stuff

* If RDD partition is lost it will recover by recomputing (all nodes knows the entire graph)
* If upstream processing is too heavy you can do checkpoints (tradeoff)
* Relies heavily on caching to be achieve high performance
* Has broadcast mechanism that can be useful to share small common datasets (avoid locality problem).
* [Accumulators](TODO) can be used for telemetry on performance tests, or error collection.
* [Broadcast](TODO) variables are useful for small datasets.
* Has logical views of [RDDs to make it SQL](http://spark.apache.org/docs/latest/sql-programming-guide.html).
* Eg. Loading a JSON as a RDD and apply a SQL logical view (visualize the structure of JSON data).
* SQL is a form of algebra, analogous to functional stuff (map/filter/etc).

On spark you have total freedom to transform data the way you want to. It is built on the idea of a
[DAG](TODO) that have a source and a sink.

The endpoints (source and sink) can be any Hadoop filesystem and also a remote endpoint.
It is pretty easy to receive data from a event source live and create an processing graph for it, sending
results to another remote endpoint or saving it on a HDFS (or other distributed filesystem).

There is no protocol defined for remote endpoints, they can be raw sockets with your data flowing on them
(fits the streaming nature of TCP).

Fault tolerance can be done with two ideas:

* Reprocess the entire graph on a new Node
* Use checkpoints (similar to hadoop synchronization)

You are always on control.

TODO: Ask Paco about the reprocess graph thing when spark is processing a live feed.


## MLlib

* Machine learning on spark
* Focused on scale, parallelism and sparsity
* Classifiers, regression
* Lot of unsupervised learning using matrix factoring
* Useful for marketing (eg, clustering for market segmentation)
* Lot of small exercises using [K-Means clustering](http://en.wikipedia.org/wiki/K-means_clustering)
* Works well with big square matrices (contributions from stanford)

There is some work on the way to add [deep neural networks](TODO DEEP MIND) 
on spark too, but it seems to be a work on progress.


## GraphX

There is a lot of support to model graphs and apply algorithms to them.

He also talked a lot about graph visualization.

Some tools related to graphs that where mentioned:

* [DeepDive](http://deepdive.stanford.edu/)
* [Titan](http://thinkaurelius.github.io/titan/)
* [D3JS](http://d3js.org/)
* Giraph
* Graphlab


## Cases

### Spotify

Spotify used Hadoop to build the music recommendation system. 

They scaled horizontaly, but the costs where getting pretty high.

The culprit is Hadoop synchronization steps that causes heavy IO.

Used [ALS Matrixes](TODO) with spark to do more with less :D.


### Pearson

Next generation adaptative learning with spark.

TODO: Get from presentation


### Yahoo

Hadoop and Spark together.

TODO: Get from presentation


### Common pattern

Use kafka to connect clusters of spark streamers and save results on cassandra.


## Projects

Some projects mentioned that I found interesting:

* [Pandas](http://pandas.pydata.org/)
* Drill
* Impala
* Storm
* parquet


## Talks


## Interesting Papers

