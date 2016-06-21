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


- Splice used to make new defs update the README on their first day.
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

