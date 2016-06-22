Dockercon 2016
--------------
######Mon Jun 20 2016

Note: <a href="slides.html?events/2016/06/dockercon16.md#!">View this as slides</a>



General session: Day 1
----------------------
- highlighting kids usage
- dockercon14: 500 attendees
- dockercon15: 2000 attendees
- highlighting community


- The best tools:
  1. Get out of the way
  2. Adopt to you
  3. Make the powerful simple
- Visual Studio debugs node.js app in a container, on a mac


- Splice used to make new devs update the README on their first day.
- Docker for Mac is easy enough they just `docker-compose up`
- Docker solved orchestration in 1.12
- Swarm mode doesn't need an external K/V
- Swarm mode knows about services now


- Swarm nodes know how to load-balance containers
- Swarm supports changing image of service in a few different ways.
- DAB file format Distributed Application Bundle
- Docker Compose generates the DAB file
- Docker for AWS beta uses cloud formation



Golden Ticket
-------------
Aaron Grattafiori @dyn__

- He wrote a whitepaper with more info.
- "Microservices distribute complexity"
- Layer defenses, harden what has to be exposed
- Microservices actually make this easier
- "Complexity breeds insecurity"


- Don't just setup TLS, but also ipsec, if you can
- TODO Research Clear Linux
- Does your OS use compile time flags for binaries?
- Default Docker AppArmor policy is good, only prevents escape from container
- aa-genprof generates apparmor profiles


- strace can be used to write seccomp profiles
- other syscall auditors: sysdig, auditd, SECCOMP_RET_TRACE
- subgraph as a libseccomp for go
- TLS all the time, everywhere, no excuses
- keep logs centrally, forever



Lunch conversation
------------------
- Tool landscape changes far too fast
- How to update?



Cloning running servers with CRIU
---------------------------------
Ross Boucher @boucher https://github.com/boucher

- http://tonicdev.com
- Tonic is a browser based REPL for node.js
- very iPythonish
- They use CRIU as you would expect, to handle editing the document after lines have been written


- Ross maintains a fork of docker on github with criu bits added
- CRIU and seccomp needs kernel >4.0.6?
- official docker repo PR #22049
- Doesn't have a good answer to how this works with the new orchestration announcements earlier



Dockerfile explosion
--------------------
Gareth Rushgrove @garethr

- ONBUILD, ARGS, etc arn't common usage
- Dockerfiles were frozen last year
- HEALTHCHECK and SHELL added in 1.12
- http://hadolint.lukasmartinelli.ch/
- words about abstractions, $LANGUAGE -> Dockerfile


- words about Docker image spec, packer, openshift, nix
- Rocker extends Dockerfiles with Rockerfiles
- Dockeramp builds images on the client
- Dockerfilepp lets users create their own primitives


- Wants:
  - Formal Dockerfile spec
  - Build API to support FROM, RUN, COPY, etc as primitives
  - Opinionated workflow tooling around image building
  - More shared libraries and preprocessors
  - Better tools for managing Dockerfiles


- Q: how to share new primitives? A hub maybe?
- Q: why freeze? Making descisions is slow and hard. Wants to see features slowly, after vetting in projects like Rocker.
- Q: how to use other tools with compose? 



Developing an Enterprise Container Management Strategy
------------------------------------------------------
Darren Shephard @ibuildthecloud

- Rancher is all open source
- business model is to sell support
- `docker run rancher/server`
- Live demo problems on a linux desktop :(
- Rancher can manage k8s, mesos, and swarm clusters
- Has a catalog of apps backed by compose or k8s that can be launched to your cluster
- Rancher 1.1 supports Docker 1.12



Reduce Devops friction with Docker and Jenkins
----------------------------------------------

- Docker can replace the .war/puppet/server bits in the usual pipeline
- Docker build and Publish, Docker Traceability, and Docker Hub Notification plugins
- Jenkns pipelne dsl dzone refcard



Security your software supply chain
-----------------------------------
Ying Li

- users, images, nodes, clusters, all have unique IDs now
- passwords aren't stored as base64 in config.json anymore
- pushing Notary
- base images are signed by Docker Content Trust


- `wget https... && echo | sha256sum`
- images expire? DCT provides this as a warning apparently
- Docker Bench is updated to 1.11
- New swarm makes the manager that is the leader handle TLS betweeen managers and nodes
- live demo of swarm with swarmkit



General Session: Day 2
----------------------

- Addressing Traditional On-Prem Legacy App
- Addressing Agile business practices
- Pushing using Docker for "Incremental Revolution"
- Demo of UCP deploying DABs, for enterprise

- https://store.docker.com
- Docker Datacenter on Azure demo
- Private Azure, on prem, talks with Public Azure, managed the same



Getting Deep on Orchestration
-----------------------------
@allingeek allingeek.com

- has experience working at Amazon
- Used Amazon Apollo, now called Code Deploy
- An orchestration platform provides control of high level abstractions which imply deployment and lifecycle management
- text heavy slides, good terminology

- Understand basic patterns, then easy to pick up any tool
- System of Record is a single point of failure
- Watch out for Network Stress
- PR question: How confident are you in these changes?

- http://principlesofchaos.org
- Project: Entropy https://github.com/allingeek/gremlins
- https://github.com/buildertools/entropy
- nifty demo



Lunch chatter
-------------

The Climate Corporation
- Nitrogen tracking
- Free weather tracking service



Making friendly Microservices
-----------------------------
Michele Titolo

- Microservice is a small service that does one thing well, that keeps up with its own data.
- Docs make microservices helpful
- Autogen Docs. Make them from the code, part of the release pipeline.
  - Swagger
  - API blueprint
  - RAML


- Be an ally by integrating monitoring tools
- Log everything, with unique IDs
- Neflix/atlas, zipkin
- Error messages are great in theory, but they have to be consistent and clear


- Mobile app gets a HTTP 206 when the server has some data
- Each service has its own container
- Stand them up with compose
- Use one base URL for everything


- Don't use wildcard certs
- Pin SSL certs
- she uses netflix/zuul for a gateway
- Need to make your API discoverable to ease the friction of others using it



20 Minutes to faking the DevOps Unicorn
---------------------------------------
Matt Williams

- "You can't just go out and buy a devops guy"
- Culture, Automation, Metrics, and Sharing
- Collect everything all the time, far too hard to recreate the problem after the fact
- recommend gathering, these work together and are almost useless alone:
  - Work metrics: Throughput, Success, Error, and Performance
  - Resource metrics: Utilization, Saturation, Error, and Availability
  - Events: Code Changes, Alerts, and Scaling Events
- Every Alert must be actionable



Serverless with Docker
----------------------
Nirmal Mehta

- Did the keynote last year, need to check into that, might be lame
- launched codelift.io last year, makes dockerfiles and compose.ymls from a github repo
- http://martinfowler.com/articles/serverless.html
- AWS launched Lambda in 2013


- serverless.com: tooling for lambda and AWS API Gateway
- iron.io: event queue, data cache, and worker components. Works in any cloud
- apex.run: framework like serverless, supports more languages than node.js with a shim.
- iopipe.com: Dockeraless, uses Swarm to run a container with the function


- thinks there will be a serverless track or section at dockercon 17
- https://github.com/iopipe/dockerbot-serverless
- Carina by Rackspace is a free 3 node swarm cluster
- https://github.com/bfirsh/serverless-docker



Sharding Containers
-------------------
Andrey Sibiryov

- Uber has 1000 microservices in production, in every language
- Comouters are basically networks-on-a-chip
- Go GC is so active NUMA logic moves memory pages closer to GC workers
- Docker can pin containers to CPU cores


- local loadbalancer, spawning and pinning multiple instances
- http://github.com/kobolog/tesson
- uses wrk for http testing
- 70% gain for free, 133/220
- gains aren't as big with python




Moby's cool hacks
-----------------

### Jeff Nickoloff @allingeek

- same project: entropy demo as earlier

### Ben Firshman @bfirsh

- Converting message queue and worker process from voting app to a "serverless" docker dingus
- Each http request is handled via a unique CGI container

### resin.io

- Yocto based OS on the drone
- Showed updating the control software on a drone while it was flying



Expo
----

### Weave

- Can be used as a Network Plugin or API proxy

### Swarm

- Multi arch cluster?
- How does the container know it's the first?
- Change environment variable, delay rollout?
- Progress of update?
- Handle Manager failure?
- How to setup 2x4 example?

### Artifactory

- How does DCT work, API?
  - Works with Notary. Dunno Notary
- How to scan and promote images, webhooks?

