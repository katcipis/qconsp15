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
When you are going to have a lot of services, making it easier to write new ones is a good ideia :-).

Also it is a good idea to leverage your products using open source stuff, like [Netflix OSS](https://github.com/Netflix).
[Asgard](https://github.com/Netflix/asgard) seems very interesting to do [Blue/Green](http://martinfowler.com/bliki/BlueGreenDeployment.html)
deployment.


## Creating a new Microservice

As said on other presentations, you start with the service interface, simple steps would be:

* Propose
* Discuss with the clients (people that are going to use your API)
* Agree

If you say, *but I still don't have any client*, well, then don't develop the service, it is pointless :-).
Cool implementation steps:

* Prototype
* Integrate with your clients and learn a lot
* **Throw away the prototype**

Until now in my life I never have seen a prototype being discarded. They usually continue being used 
(even tough they have a lot of severe design flaws and have no tests at all).

I think the main two reasons for this to happen are:

* Failure to understand that the prototype value is what you learn with it, not the code
* Failure to build a small prototype and integrate it fast

If you developed a prototype for a month and then integrated it you will be less prone to
destroy it and build a new stuff from scratch if the prototype took a week.

The cycle of developing the prototype and integrating it must be as small as possible, it is 
easier said then done, but it is a good objective.

Also Randy said that in his experience, after a prototype has been done, the work of developing the
real thing (with tests and proper documentation) does not take as much time as people think.

One of the anti-patterns more expressive on the microservices movement is database integration.
This happens when you use databases to integrate different services, instead of using well defined interfaces.
Yes, integrating services using [Redis](http://redis.io/) is still database integration :-).

I often see this kind of thing being explained as *"simpler"* than other alternatives (perhaps a REST API).
In my opinion, this fails on the [four rules of simple design](http://martinfowler.com/bliki/BeckDesignRules.html),
more specifically on the **reveals intention** rule.

I'm not a big fan of rules, but these ones are pretty cool as a baseline of what is really simple :-).


## Ownership

The team that develops the service is responsible for:

* Meeting the needs of the client (people using the API)
* Doing this at minimum cost and effort
* Design + Code + Tests + Deploy,  *You build it, you run it*
* Never break your clients code
* Use versioning and deprecation mechanisms to enable evolution

This is one of the more important aspects of developing good services, it is related to DevOps and 
prevents the traditional **the system does not work but everyone did their job so no one is responsible**
thing. If it is not working, it is the team fault (the entire team), period.


## Interesting tools

Basically a lot of cool stuff from Netflix OSS:

* [Ribbon](https://github.com/Netflix/ribbon)
* [Histrix](https://github.com/Netflix/Hystrix)
* [Eureka](https://github.com/Netflix/eureka)
* [Asgard](https://github.com/Netflix/asgard)


## Conclusion

It was a great presentation, it showed clearly that microservices is more a cultural change than a technology thing
involving the size of your services.
