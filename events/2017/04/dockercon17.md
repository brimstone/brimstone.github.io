Dockercon
-------------
######Tue Apr 18 2017

Note: <a href="slides.html?events/2017/04/dockercon17.md#!">View this as slides</a>



Keynote Day #1
--------------
- general "Where we're from"
> "My containers are too big!"

  - multistage builds
> "Make it easier to go from desktop to cloud"

  - Can do with Docker Cloud, Docker Swarm, and Docker For Mac/Windows
  - Atsea Shop Demo of multistage build, Docker Cloud, and Swarm integration
  - Features in Edge release now


- For ops:
  - Swarmkit: addresses secure communication and secrets
  - not limiting developer choice and still secure app
  - Atsea Shop Demo of deploying to prod, Swarm, labels, failure actions
- Announcing LinuxKit
  - lean
  - everything is a container
  - secure patches and config targeting container based workloads
  - Sounds a lot like rancherOS


- Microsoft is now supporting Linux containers in hyperV on Windows now
- Live release of [LinuxKit](https://github.com/linuxkit/linuxkit)
- Docker is building assemblies like car plants, for each of their OSS components
- Announcing the Moby Project for managing these assemblies
  - moby seems to replace packer


- weekend projects:
  - locked-down linux with remote attestation
  - custom ci/cd stack with linuxkit and infrakit
  - custom ci/cd stack with debian and terraform
  - RedisOS Demo
  - etcd cluster on GCP
  - kubernetes on mac

Note: - The demos are extremely polished and target management as well as engineers


Diversity on the Face of Adversity
----------------------------------
Kate Hirschfield - @K8Hir

- It's not a pipeline problem
- People like her don't want to go into tech because people like her aren't in tech
- [Banned presentation](http://bit.ly/HCMSLGBT)
- 1 Create a culture on purpose
  - talk about respect
  - talk often
  - managers need to make their beliefs clear and employees will follow
  - Caroline Boudreaux's "No Asshole Policy"


- 2 Make Zero Tolerance real
  - Passiveness is acceptance
  - Think about how you'd handle an offense if you saw it happen
- 3 Prioritize Diversity
- How do we start this?
  - connect role models to people possible "in the pipeline"
  - a sense of belonging gets people to stay
  - it's not going to be easy


What I wish I knew when I was 12
--------------------------------
Finnian Anderson http://finnian.io/blog

- Before Docker
  - vcs is hard
  - conflicts between apps
  - some apps are just really small and overkill on a full system
- With Docker
  - using portainer.io
  - load balancing demo with servos!
- After Docker
  - fleetreach.co.uk


What's new
----------
Victor Vieux

- New version number
  - stable quarterly releases
  - monthly less stable releases
- Builder in 17.05
  - build args can be used in from tags!
- Data management commands in 17.03
  - `docker system df`
  - `docker system prune`


- New plugin system in 17.03
  - `docker plugin install` pulls from the Hub or private
- Swarm commands can be synchronous now in 17.04
  - `docker swarm --detach=false`
- Swarm can now rollback, pause, and continue in 17.04
- Swarm can prefer topology in 17.04
  - `docker swarm --placement-pref-add=rack`
- Compose to swarm in 17.03
  - `docker stack`


- Compose v3 in 17.03
  - removed non portable options like host volumes
  - added swarm attributes like replicas
- Compose has long support for ports in 17.04
  - microformat: 9090-9095:8080-8085
  - targets: 9090-9095
  - published: 8080-8085
  - protocol: tcp
  - long syntax for volumes too


LinuxKit
--------
Justin Cormack, Nigel Edwards, Ilya Dmitrichenko @errordeveloper, Dave Freita

LinuxKit
- foundations in immutable delivery
- built for desktop editions first
- keeping with the "batteries included, but removable" mantra
- rebuilding services in rust
- InfraKit manages clusters


- InfraKit alternatives, Terraform, CloudFormation
- GCP, kvm, vmware support
- AWS, Azure, arm64 support in progress
- uses runc/containerd and not docker


Linux-oKernel Demo
- Inner Kernel: <5k LOC, hardware access, physical memory
- Outer Kernel: everything else
- 3~5% performance increase
- `cat /proc/self/okernel`
- demo breaks container isolation to steal memory secrets


Kubernetes Demo
- moby loads images into the OS at boot time

BlueMix Demo
- ran docker on linuxkit
- works with bluemix
- builds a vmdk that is converted to vdi by virtualbox


Questions
- can build AMIs with a little help
- shipping production ready this quarter


Everything you thought you knew about orchestration
---------------------------------------------------
Laura Frank @rhein_wine

- The big problem is to get many nodes to work like one node
  - state
  - scheduling
- Quorum must be understood
  - Use odd numbers of managers
> "I literally can't even"


- Raft is an algorithm for distributed systems. Don't write your own.
- Don't run work on your manager nodes
- Raft demo, http://demo.consensus.group https://github.com/ongardie/raftscope
- the nodes keep a log of truth
- [Understand Logging](http://bit.ly/logging-post)
- can force swarm to rebuild with --force-new-cluster


What have namespaces done for you today?
----------------------------------------
Liz Rice - @lizrice

- See this demo


OCI Standards panel
-------------------

- The Runtime Spec is pretty solid
> "Much like the HTML spec doesn't define best practices for writing good webpages, the OCI spec doesn't define best practices for building good container images."

- Security is out of scope for OCI



General Session Day #2
----------------------
- teaser about the logo
- Day 2 is about Docker in the Enterprise
- ETR Survey shows Docker has super
- Visa devs deploy to prod on day one
- Demos and segments are very business oriented


Lightning Unikernels
--------------------
Michael Bright

- why? Only features you need, better for security and performance
- can boot in 100s of ms
- use cases: NFE (Telco Cloud)
- implenteations: clean slate or legacy
- Legacy OSv for Go; Rumprun/LKL for Ruby, Go, and Python; Ultibo for rpi
- MirageOS: `make configure -t (unix|ukvm)` then just ./ the binary


It takes a village
------------------
Jeff Lindsay @progrium

- pretty neat, docker containers behind ssh-aaS
- `ssh cmd.io http`
- released an ssh server library
- https://github.com/gliderlabs/ssh


From Zero to Docker Hackathon Winner
------------------------------------
Jimena Tapia @tapiajimena, Marcos

- Met docker via a personal project
- Whaleprint lets you know and see what will happen when you deploy to Swarm
- Focus on an MVP in the hackathon
- Take the final user into account
- Make you thing easy to understand


Plugins
-------
Nandhini Santhanam, Tibor Vass

- Plugins first class in 17.03
- Auth, Volume, Logging, IPAM, Network
- Demo building sshfs plugin
- plugins implement something like docker.volumedriver/1.0
- debug `tail /var/log/docker.log | grep plugin=`
- Plugins are containers. They run under containerd and runc.
- plugins listen on a socket in /run/docker/plugins
- [Go helper library](https://github.com/docker/go-plugins-helpers/volume)
- `docker plugin create`, then `docker plugin push`


From ARM to Z
-------------
Christy Perez, Chris Jones tophj-ibm

- s390x/ubuntu, aarch64/ubuntu
- https://hub.docker.com/u/multiarch
- https://github.com/multiarch/qemu-user-static/releases
- in Go build tags, spaces are ORs, commas are ANDs
- estesp/manifest-tool, docker PR #27455
- `docker manifest push -f multi.yaml`


Cloud Native Future
-------------------
Panel

- members: Kubernetes, Prometheus, OpenTracing
- https://www.cncf.io
- OpenTracing allows you to view every point of code and infra a request touches
- Twitter coined [Googwin](http://www.urbandictionary.com/define.php?term=Googwin)
- containerd uses grpc and has a prometheus endpoint
- survey of the room, prod scheduler: k8s, swarm, nomad, mesos
- OpenTracing is working on RabbitMQ support
- 


Moby's Cool Hacks
-----------------

Marcos Niles @marcosnils, Jonathan Leibiusky @xetorthio, sherloq.io
- Showing off play-with-docker.com
- export PWD_URL, `docker-machine -d pwd`
- The UCP works with play-with-docker.com too
- They do Swarm in Swarm

Alex Ellis @alexellisuk
- get-faas.com
- Functions-as-a-Service



Moby Project Summit
-------------------

Intro & General Q&A
- Clarifying role of containerd, by Docker, for CNCF
- Docker was used as a component in other systems. Containerd should be used instead.
- People has asked to work on the project without working on the product
- Docker is moving projects out of the company and under the moby org until they're split off completely into their own org.
- docker is built with moby
- `docker` is moving back to github.com/docker/cli soon
- `docker` defaults to pulling from the hub. `containerd` has no default
- `moby` is a build tool for bootable systems or services like docker
- They're not completely committed to Go now that components are breaking out. Ocaml and Rust are also mentioned for systems things
- gRPC will allow for more automated tooling. They're working out how to switch the Docker HTTP API to gRPC

containerd progress
- super short

SwarmKit progress
- Today, SwarmKit ->  docker engine -> containerd. Soon, removing docker engine
- new generic runtime: ask for 10 units and a plugin will handle creating each one
- SwarmKit is gRPC heavy too

LibNetworking progress
- want to integrate with containerd more too

Notary progress
- something about securing files from the layers after they've been extracted
- sounds like notary is moving to moby

Infrakit
- seems to compete directly with terraform
- hope to have a stable API by 1.0
- stuff is moving/changing very fast
- dunno if they're moving under moby
- they want to integrate with k8s better

Infinit
- an aquisition at the end of 2016
- storage platform
- a K/V store allowing for object store and popular storage API abstractions
- closed source, for now
- doesn't use moby, has their own build system: drake

MirageOS
- version 3.0 is much nicer
- announcing MirageSDK
- SDK supports OCaml, next rust, later webassembly, never C
- first DHCP client, next NTP client
- demo the dhcp client is storing lease information in a git repo on disk for the privilaged container to parse and affect change on the kernel


LinuxKit BoaF
-------------

- LinuxKit is just a library of components
- the `moby` build tool needs to move out of linuxkit/linuxkit
- `moby` will eventually produce the `docker` packages
- no good ISO9660 lin for go, so they use a container for mkisofs



Organizer Summit
----------------
- pushing the Docker in Higher Ed program
- Students get 1 node and 5 private repos in Docker Cloud for a year
- The Mentor program is much more established now
- Mentor summit was recorded
- A small percent of mentors show up to meetup events, trying to fix that
- Organizers can be mentors, expected to be advanced to expert level


Play with docker
----------------
- training is a jekyll github page under fanela org
- tutorials are super slick
- there is an SDK you can embed n any site
- can be run locally with `docker-compose up`
- lots of discussion about problems and feature requests


Organizer date
--------------
- new city centric page off docker.com
  - list of captains, organizers, and mentors
  - possible renaming of Organizers
- mascot! Octopus, dolphin balancing things, seal
- the captain seagull doesn't have a name


Meetup Tips
-----------
NYC organizers

- tools:
  - google forms for surveys and talk suggestions and speaker sign up
  - keep checking commnity repo and labs
  - they email out reminders about meetups
- keep asking for sponsors, mentors, speakers
- scratch other meetups and get them to scratch yours
- co-meetups seem to help grow membership the best
- ask new speakers for an abstract or the whole slide deck to make sure they're educatun focused and not product focused
- get product presentations to present use cases
- ask sponsors from similar meetup groups

Welcoming women to your meetup
------------------------------
Patty GirlDevelopIt

- Code of Conduct, don't just check it off a list
  - make it easy to report misconduct
  - don't relay on victims reporting
  - everyone must be aware
- First Impressions
- Reach out to new members
- Introduce new members to others
- Encourage women speakers
  - Impostor syndrome
  - assist in dry-run, review content, and constructive feedback
  - create list of previos talks/videos
  - suggestions for talk topics
- how to reach out as a man:
  - Karen can help introduce to girldevelopit in your area


Community Code of Conduct
-------------------------
- mention coc at the start of meetups
- make sure people know how to contact you to report
- we don't need permission to eject or ban a member
- 
