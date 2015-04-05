# Architecting for high load

At the start it would look like this presentation would be
all about [Aerospike](http://www.aerospike.com/).

I was kinda surprised by the fact that it actually didn't :-).
Of course there was some talk about aerospike later, but great part of the 
presentation was about how to architect systems for high load, really good stuff like:

* [Little's law](http://en.wikipedia.org/wiki/Little%27s_law)
* Queueing Teory
* Throughput considerations
* Latency
* Concurrency
* Bottlenecks
* Locks and critical regions
* [NUMA](http://en.wikipedia.org/wiki/Non-uniform_memory_access)
* Detailed explanation of how SSD works :-)

The presentation job was to lay down a basis to explain how Aerospike can be
totally awesome and faster than anything :P.

Of course there is a desire to sell stuff, but some things seems to be really different about Aerospike.
One of them is the smart client idea.

For example, on Cassandra, the client is dump and it talks with a coordinator. The coordinator does the writes, knows
the cluster, participates on gossiping and [paxos](http://en.wikipedia.org/wiki/Paxos_%28computer_science%29).

On Aerospike the client is the coordinator (that is why the client is *smart*), it is aware of the cluster and it
contains all knowledge required to perform a read/write directly on the nodes, it does needs to talk with a coordinator.

This makes the client API more complex, but enables smaller latencies since the client talks directly to the nodes
responsible for storing the data.

Besides lower latency, Aerospike enables a decentralized approach where adding nodes is automatic, there is no 
master/slave to solve. The configuration of all nodes is the same. You only have to know one node to get in the cluster
(any node).

It uses a variation of Paxos to decide which nodes are part of the cluster and a variation of the
[Gossip protocol](http://en.wikipedia.org/wiki/Gossip_protocol) to heart beating.
They implemented a variation because they saw some opportunity to optimizations on the protocols (and it is 
open source, got check it out !!! :D).

Determining the partitioning of data is done through paxos. The smart client is aware of all this.

Another interesting idea behind Aerospike is the optimization for SSD disks. AFAIK every time you focus on supporting 
*one* thing (in this case, SSD) instead of two (disks and SSD) you get the opportunity 
to do some interesting optimizations.

And guess what ? They did it :-). Some key points on how data is handled on the SSD disks:

* Bypass the filesystem
* Threats the SSD as a gigantic RAM memory, doing writes contiguously on the *memory*
* Copy on write (he talked about log structured writes, reminds me of LSM)

All this made on C (not C++, C :-), using [jemalloc](https://www.facebook.com/notes/facebook-engineering/scalable-memory-allocation-using-jemalloc/480222803919).
They showed some great concern about performance and showed great technological knowledge, it seems really promissing :D.
The project has been [open sourced](http://www.aerospike.com/docs/architecture/) recently.

There is a more detailed [documentation about the architecture](http://www.aerospike.com/docs/architecture/).
The only annoying thing is all the talk about *ACID* which we [know](http://en.wikipedia.org/wiki/CAP_theorem) 
it is bullshit :-) (or they have some miraculous implementation of Gossip/Paxos).
On the end it guarantees partitioning and availability :-).
