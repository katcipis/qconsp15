# From the monolith to microservices

On [this presentation](http://qconsp.com/presentation/monolith-microservices-evolving-your-architecture-scale)
Randy Shoup started presenting the pros/cons of a Monolith (which was pretty cool).

Monolith pros:

    * Simple at first
    * In proc latencies (pretty low)
    * Single codebase and deploy
    * Resource efficient (at small scale)

And then, the cons:

    * Coordination overhead as teams grows
    * Poor enforcement of modularity
    * Poor scaling
    * All or nothing deploys
    * Long builds
    * Hard to tune databases
    * All or nothing schema management

So he started to talk about how things usually to do not start beautifully as microservices, I liked a lot
of this sentence:

** If you don't regret your early technology decisions, you over designed **

Well, it was something like this, I found it pretty cool, then he said something like if Google started with
microservices they would not even exist. It helps you understand that if you are working to break a monolith
this is just part of the development process, it does not mean that everyone was a complete retard before :-).

He talked about the old three tiers design and how microservices resemble more a graph of services instead of
a tier design. I still think that a [four tier design](http://nginx.com/blog/time-to-move-to-a-four-tier-application-architecture/)
exists on microservices, since you have to aggregate and deliver the results to the client. The graph resides
on the services tier.

Finally someone else agreed with me that Microservices is just SOA done properly :-). When the whole microservices
thing started I was having a lot of trouble trying to understand what was the difference from microservices and
SOA. After reading [this great article from Dan North about SOA](http://dannorth.net/classic-soa/) I was able to understand
that the difference does not exist.

The distinction emerged from the fact that SOA often reminds people of technologies like SOAP and the WS-Deathstart set 
of... crap :-) (sorry I can't think on a better name for the whole WS-\* thing).

But in fact the idea of SOA has nothing to do with technologies, as Dan article explains beautifully.

Some other important points:

    * Isolated persistence
    * No centralized top-down design of the entire system
    * No architect centralizing decisions
    * Standarize network protocols, data formats and interface schema specification

The standardization thing is important, basically if you see microservices as a graph, you must standardize the 
arch's of your graph.

People often talks about how microservices is the philosophy of Unix services reborn, if you don't standardize the 
communication and keep this communication simple you are not going to reap the same benefits that
Unix has been reaping so far.

He said something about creating services chassis, reminded me a lot of 
[Tailored Service Template](http://www.thoughtworks.com/radar/techniques/tailored-service-template), makes sense.

Also it is a good idea to leverage your products using open source stuff, like [Netflix OSS](https://github.com/Netflix).
[Asgard](https://github.com/Netflix/asgard) seems very interesting to do [Blue/Green](http://martinfowler.com/bliki/BlueGreenDeployment.html)
deployment.
