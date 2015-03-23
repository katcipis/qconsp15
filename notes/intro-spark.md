#Intro

* A lot of jabah from databricks about their notebook thing, that is like google docs
* Has stuff like visualization of data (d3js)
* Loves functional programming (Clojure) :-)
* Lazy evaluated, just builds graph with transformations and wait action to start evaluation.
* Filtering / lambda based
* Pipeline based, makes good use of cache, works on memory
* Well suited to functional programming, map and filtering builds a graph
* Remove synchronization using function composition and algebra :D
* A program is a collection of functions working on arrays of data.


## MapReduce x Spark

* MapReduce if for fault tolerance (eg. disk failures on jobs that takes 24 hours)
* MapReduce is made for commodity hardware from 2002
* Changes like multicores, more memory, SSD, faster networking.
* Spark tries to leverage this
* MapReduce is hard to understand (hive, pig to make it easier).
* Instead of using a lot of clusters and tools converge it to one core supporting different programing models.
* Hadoop has synchronization barriers (reduce/merge phase), Spark avoids this partitioning data by key


## Design and stuff

* Runs native Python, you have to provision the node with libraries, but it does not run on the JVM.
* If RDD partition is lost it will recover by recomputing (all nodes knows the graph)
* If upstream processing is too heavy you can do checkpoints (tradeoff)
* Accumulators can be used for telemetry on performance tests, or error collection.
* Broadcast variables are useful for small datasets.
* Has logical views of [RDDs to make it SQL](http://spark.apache.org/docs/latest/sql-programming-guide.html).
* Loading JSON as a RDD and apply a SQL logical view.
* Enables you to use SQL and visualize the structure of JSON data.
* SQL is a form of algebra, analogous to functional stuff (map/filter/etc).


## Math

* functional programming and algebra, [Algebird !!](https://github.com/twitter/algebird)
* The idea of use monoids as a container for functions, if the function is a monoid the details are irrelevant.


## MLlib

* Machine learning on spark
* Focused on scale, parallelism and sparsity
* classifiers, regression
* lot of unsupervised learning using matrix factoring
* useful for marketing (eg, market segmentation)
* lot of small exercises using [K-Means clustering](http://en.wikipedia.org/wiki/K-means_clustering)
* works well with big square matrices (contributions from stanford)


## GraphX

* Cool example solving the shortest path possible from two nodes.


## Cases

### Spotify

Spotify used Hadoop to do music recommendation. Wanted to cut costs.

Hadoop has a lot of synchronization steps that causes heavy IO.

Used [TODO]() with spark to do more with less :D.


### Pearson

Next generation adaptative learning with spark.


### Common pattern

Use kafka to connect clusters of spark streamers and save results on cassandra


## Projects

* [D3JS](http://d3js.org/)
* [Pandas](http://pandas.pydata.org/)
* Giraph
* Graphlab
* Drill
* Impala
* Storm
* parquet


## Talks


## Interesting Papers


