Dockercon 2016
--------------
######Mon Jun 20 2016

Note: <a href="slides.html?events/2016/06/dockercon16.md#!">View this as slides</a>



General session
---------------
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




