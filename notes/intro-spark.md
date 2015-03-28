#Intro

* Lot of love for functional programming (Clojure) :-)
* Stream processing is graph based.
* Streaming graph is lazy evaluated, just builds graphs ([DAG](http://en.wikipedia.org/wiki/Directed_acyclic_graph) )
  with transformations and wait action to start evaluation.
* Core concept is a collection of functions working on arrays of data.

The workshop presentation can be found [here](http://training.databricks.com/workshop/sparkcamp.pdf).


## MapReduce x Spark


Some ideas:

* MapReduce was made for fault tolerance (eg. disk failures on computers from 2002)
* MapReduce is made for commodity hardware from 2002
* Changes like multicores, more memory, SSD, faster networking changed the game.
* Spark tries to leverage these changes with a graph streaming model.
* MapReduce is hard to understand (hive, pig and other frameworks try to make it easier).
* MapReduce programming model is very narrow (again that is why a lot of frameworks works on top of it).
* Hadoop has synchronization barriers (reduce/merge phase), Spark avoids this by giving you control of checkpoints.
* Sparks runs the native language (Scala, Java and Python), 
  you have to provision the container with libraries, but it does not run on the JVM (no indirection).

I understood that Spark provides a more flexible programming model. You are not constrained
by map / reduce phases.

Since Hadoop was built on the idea of fault tolerance on a time that disk failure was high and memory was more
expensive it does a lot of heavy I/O, this leads to a poor performance when you compare hadoop with spark
(on some cases).

Later on there will be a interesting use case from spotify that relates to this idea.


## Design 

* If RDD partition is lost it will recover by recomputing (all nodes knows the entire graph)
* If upstream processing is too heavy you can do checkpoints (tradeoff)
* Relies heavily on memory caching to be achieve high performance
* Also relies on commutativity and associativity of functions to enhance parallelism.
* Has broadcast mechanism that can be useful to share small common datasets (avoid locality problem).
* Process real time streaming as small batch jobs (with time windows).
* Great potential to combine batch and streaming processing on the same system.
* [Accumulators](http://spark.apache.org/docs/1.2.1/programming-guide.html#accumulators) can be used for telemetry on performance tests, or error collection.
* [Broadcast](http://spark.apache.org/docs/1.2.1/programming-guide.html#broadcast-variables) variables are useful for common input datasets.
* Has logical views of [RDDs to make it SQL](http://spark.apache.org/docs/latest/sql-programming-guide.html).
* Eg. Loading a JSON as a RDD and apply a SQL logical view to visualize the structure of JSON data.
* SQL is cool :-) (its algebra), analogous to functional stuff (map/filter/etc).

On spark you have total freedom to transform data the way you want to. It is built on the idea of a
[DAG](http://en.wikipedia.org/wiki/Directed_acyclic_graph) that have a source and a sink.

The endpoints (source and sink) can be any Hadoop filesystem and also a remote endpoint.
It is pretty easy to receive data from a event source live and create an processing graph for it, sending
results to another remote endpoint or saving it on a HDFS (or other distributed filesystem).

There is no protocol defined for remote endpoints, they can be raw sockets with your data flowing on them
or other protocols like ZeroMQ or Flannel.

Fault tolerance can be done with:

* Reprocess the entire graph on a new Node
* Using checkpoints (similar to hadoop synchronization)

You are always on control on the tradeoff or recomputing failed nodes or doing synchronization.


### MLlib

* Machine learning on spark
* Focused on scale, parallelism and sparsity
* Classifiers, regression
* Lot of unsupervised learning using matrix factoring
* Useful for marketing (eg, clustering for market segmentation)
* Works well with big square matrices (contributions from stanford)

There is some work on the way to add [deep neural networks](http://deepmind.com/) 
on spark too, but it seems to be a work on progress.


### GraphX

There is a lot of support to model graphs and apply algorithms to them.

He also talked a lot about graph visualization tools.

They are all listed on [Tools](#graphs).


### Cluster management

Spark comes with a few [cluster management options](http://spark.apache.org/docs/1.2.1/cluster-overview.html#cluster-manager-types).

Spark has mesos integration, and it seems to be an [integration between mesos and kubernetes](https://mesosphere.com/2014/07/10/mesosphere-announces-kubernetes-on-mesos/).

The project [kubernetes-mesos](https://github.com/mesosphere/kubernetes-mesos) seems interesting, 
but it is a work in progress right now.


## Cases

* [Twitter](http://www.slideshare.net/krishflix/seattle-spark-meetup-spark-at-twitter)
* [Spotify](http://www.slideshare.net/MrChrisJohnson/collaborative-filtering-with-spark)
* [Stratio](http://spark-summit.org/2014/talk/stratio-streaming-a-new-approach-to-spark-streaming)
* [Pearson](https://databricks.com/blog/2014/12/08/pearson-uses-spark-streaming-for-next-generation-adaptive-learning-platform.html)
* [Ooyala](http://spark-summit.org/2014/talk/productionizing-a-247-spark-streaming-service-on-yarn)
* [Guavus](https://databricks.com/blog/2014/09/25/guavus-embeds-apache-spark-into-its-operational-intelligence-platform-deployed-at-the-worlds-largest-telcos.html)
* [Ebay](http://www.ebaytechblog.com/2014/05/28/using-spark-to-ignite-data-analytics/)
* [Yahoo](http://spark-summit.org/talk/feng-hadoop-and-spark-join-forces-at-yahoo/)
* [Databricks customers](https://databricks.com/resources/customer-case-studies)

## Projects

Some projects mentioned that I found interesting:

* [Pandas](http://pandas.pydata.org/)
* [Drill](http://drill.apache.org/)
* [Impala](http://impala.io/)
* [Parquet](http://parquet.incubator.apache.org/)


### Graph

* [Giraph](http://giraph.apache.org/)
* [DeepDive](http://deepdive.stanford.edu/)
* [Titan](http://thinkaurelius.github.io/titan/)
* [D3JS](http://d3js.org/)
* [Graphlab](https://dato.com/products/create/open_source.html)


## Talks

* [The Spark SQL Optimizer and External Data Sources API](http://youtu.be/GQSNJAzxOr8)


## Interesting Papers / Presentations

* [Scala Crash Course](http://lintool.github.io/SparkTutorial/slides/day1_Scala_crash_course.pdf)
* [Introducing DataFrames in Spark for Large Scale Data Science](https://databricks.com/blog/2015/02/17/introducing-dataframes-in-spark-for-large-scale-data-science.html)
* [Efficient Data Storage for Analytics with Parquet 2.0](http://www.slideshare.net/julienledem/th-210pledem)
* [Discretized Streams: A Fault-Tolerant Model for Scalable Stream Processing](http://www.eecs.berkeley.edu/Pubs/TechRpts/2012/EECS-2012-259.pdf)
* [A Few Useful Things to Know about Machine Learning](http://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)
* [Pregel: Large-scale graph computing at Google](http://googleresearch.blogspot.com.br/2009/06/large-scale-graph-computing-at-google.html)


## MOOCS

* [Scalable Machine Learning](https://www.edx.org/course/scalable-machine-learning-uc-berkeleyx-cs190-1x#.VRb_g-nd_0o)
* [Introduction to Big Data with Apache Spark](https://www.edx.org/course/introduction-big-data-apache-spark-uc-berkeleyx-cs100-1x#.VRb_fend_0o)
