#TODO

The Introduction to Spark ended pretty early, so I had time to take a look on the end
of Rand Shoup presentation.

It was pretty interesting, some stuff that people are already talking about for a long time.


## Interfaces and Services

* No mega services (doh)
* Dont use databases to do integration (lack of encapsulation and opens backdoors)
* SOA = Microservices, finally someone thinks like me :D
* Prototyping = Learning. Throw away the code (This one is from Pragmatic Programming :-)


## When to start using microservices ?

There is a cost involved on developing microservices, to a startup with 6 people it may not seem
to be interesting to have a lot of different services with different databases and technologies
(and deploys, even if automated :-).

You have to be realistic with the amount of resources you do have.

But when you do start to invest on breaking stuff apart ? Basically when people starts to trip on each
other feet and the big thing starts to slow you down.

This idea reminds me of Adrian Crockfort [talking about how microservices started at Netflix]().
He said the same things... made sense. It is interesting that he even said that the problem was not 
software scalability, the problem was scaling the development, too much people messing around on the
same software without good boundaries separating stuff.

More interesting talks from Adrian:

TODO (microservices stuff 1 and 2 :-)

On the end there was a good question to introspection, *how much does the monolith bothers you ?*

This should guide how much effort will be done on splitting it.


## Testing

When stuck with legacy code he said that the best option is to functional testing. 
Focus on tests that aggregates good value to the business.

Unit tests have great value, but if you are going to have only 6 tests, they must be acceptance tests.

Also he talked about a pattern of incremental improvement that I already read before and find really 
interesting. It is pretty simple:

* When a bug is found, you correct it with a test.
* New features comes with tests only.

This way you can start fighting back against entropy. This is a simple idea but on some cases is pretty hard
to put in practice :-).

It is important to always move forward, none of the tests must be left broken or be removed.

The steps are small and always forward :-).
