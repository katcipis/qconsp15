# Living DevOps beyond infrastructure automation

This was a very interesting talk since it discussed devops as a cultural change,
not only automating stuff (although automation is important).

The case that has been discussed was a migration from [MPS.BR](http://www.softex.br/mpsbr/) and
[CMMI](http://cmtitute.com/) to an agile approach.

There was the basic ingredients, lots of process and slow development...including the traditional
estimation process.

When trying to implement SCRUM they had several problems, like mindless daily meetings (I personally
also lived this kind of sad situation :-(). Things was still not getting better.

Only when they started to implement a cultural change, coming from development practices, that they
started to get some results.

They started with [Extreme Programming](http://www.extremeprogramming.org/). Besides the benefits of
focusing on tests and code quality, they said that the most important thing was the change on
the *mindset*.

This makes perfect sense with the ideas of [SCRUM](https://www.youtube.com/watch?v=AuUadPoi35M)
without its many barnacles.

Other points that where important to real change where:

* Coaching
* Retrospectives (good SCRUM again :D)
* Internal talks and workshops

Basically one of the most important things that agile tries to solve, communication :-).
They had a lot of barriers on the communication (processes) and people where isolating from each
other behind those walls.

When stuff gone bad, no one was responsible.

They also talked about ops participating on the architecture definition, again this makes total sense
with XP sense of an entire team working together, without predefined papers (tester, architect, developer, ops, etc).

They talked a lot about monitoring and stress testing, which reminded me a lot the book 
[Release It!](https://pragprog.com/book/mnee/release-it).  The idea is to anticipate problems, 
you cant anticipate all problems (that's why delivering soon is important), but it is good
to anticipate stupid stuff with good testing :-).

On the end they talked about quick wins:

* Build a deploy pipeline
* Treat infrastructure as code (no [snowflake servers](http://martinfowler.com/bliki/SnowflakeServer.html) )
* Automate everything
* Stress testing + monitoring

On the end they talked about how before working software was enough (the code is done and the tests pass).
Now this is not enough anymore, it must be deployed and in production...or it is *NOT* done.
