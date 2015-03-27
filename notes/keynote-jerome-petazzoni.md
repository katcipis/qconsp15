# Wednesday Keynote - Jerome Petazzoni

Problems got harder, ops can fix them and devs cant anticipate them.

Here enters DevOps:

* Same team as devs (no devops team please :-)
* Everyone on call (yes, that includes YOU developer :-)
* Ubiquitous automation
* Deploying cant be slow or dangerous (doh, great automation)

Some things that I found specially cool.


## Blue / Green deployment

He started to talk a little about [Blue/Green](TODO) deployment.

Working with a strategy like that is pretty cool and enables faster deployments
since you don't have to be afraid of problems, since rolling back the update 
is easy.

But when working with images this setup is pretty slow. Working on this approach
with containers is much more feasible (think on green / blue containers :-)


## Development Environments

I was already working with docker to enable better development environments
(actually I was copying their development environment :-), and any development environment
must enable a easy way to build and run tests.

Sometimes a service that you are developing depends on other services to run and 
[docker compose](TODO) provides a very declarative way to do that.
Using [linking](TODO) docker compose enables something like service discovery
for your development environment.

Using tools like docker compose is specially important when you are working with
microservices, where a lot of different languages and tools are involved on
building a proper development environment.


## Testing

Tests must be [FIRST](TODO), and docker enables this easily. For a good case of this
take a look on the docker project itself, pretty cool what they have going on there :-).

But there is something that caught my atention because it is a problem that I have been
exposed recently, testing code that depends on databases.

Well, unit tests should not depend on a database, but you will need integration tests
(end to end, smoke, stress, etc) that will depend on the integration with the database.

I know 2 ways to do that.


### The One Database

Here we have a central database that is used for testing. All testing that 
requires integration will use this database.

This one seems fast and simple at the start, the main problem is that compromises the 
isolation of the tests. Everyone messing around on one database is a recipe for disaster,
specially on testing, where things will usually go wrong and the database may be left 
on a very odd state.

If your tests gets non deterministic, you have a [problem](TODO).
Non deterministic tests are worse than no tests, because they don't help you and effectively
waste your time.

The database could be read-only, but that would not contemplate all scenarios of a integration test.

Also with a writable database it would be hard to execute acceptance tests on parallel on some cool CD/CI tool,
it would be even easier to something go wrong.


### Multiple Databases

The obvious alternative is creating a copy of the database (a read only snapshot) 
to do your tests and when you are done you can trash it.

This will give you isolation from others tests, you gain speed on parallelization but it is kinda
obvious that copying around databases is not very fast...and this would be part of your fixture.

Depending on the size of the dataset you need this could be extremely prohibitive... until docker :D


### Multiple Databases + Docker magic

This one will be pretty fast :-). Basically build a base image with your database (and data)
and execute containers from this base image.

This is exactly the idea of copying around databases, the gain you get is docker copy on write
and read-only base images.

Since the base image layer is ready only you can be confident that no one can mess around with the
test database. Everyone can "copy" it around, nothing will be actually copied until you start to
write stuff.

Basically you get all the benefits of multiple databases without the performance penalty.
Another example of docker awesomeness :-).

A CI/CD would be able to run a lot of concurrent tests, all using its own instance of the same database,
without using a lot of resources. And the writes happens only on the container layer, completely isolated
from the other tests.


## Managing a cluster


Jerome mentioned the possibility of using [docker swarm](TODO) + [mesos](TODO) where
docker swarm offloads jobs to mesos.

A complete solution of service discovery and clustering is a work in progress.


## Tools

Some tools mentioned along the presentation

### Flannel

### Pipework

### Flocker

### CRIU
