Openstack Summit
----------------
######Mon May 12 - Wed May 15 2014

Keynotes:
- This place is huge.
- Ops meetup sounds interesting
- "Everyone competes with a startup"

Wells fargo guy
- KYC
- "software defined economy"
- drills in using Openstack to enforce compliance.

Disney guy
- good, fast, cheap now just fast, fast, fast
- "you shouldn't be more efficient at home than at work"
- shadow IT shows you where to improve

Rackspace
- Defcore
- is apparently making bank
- might be a better option than Scalematrix?
- "we like to argue." re: trust, leadership of openstack

Dell
- rock tumbler metaphor about conflict
- strong "arguing is good" vibe
- brought up HyperV.

- There's an O'Reilly book: Openstack Operations Guide
- Superuser.openstack.com


Orchestration
-------------
Heat
Like config mgmt, but for infrastructure
Puppet and juju are mentioned, not chef
Templates result in stacks, can depend on other stacks
Templates are: parameters, resources, outputs
Resources are properties and attributes
Similar to cloud formation language
Screens of text
Github.com/hardys/demo_templates
Icehouse is much better than previous releases

libvirt
-------
Ceo of metacloud
Nova uses libvirt which uses qemu which, as of 1.3, is kvm
Guy is sad when you use swap in VMs
- memory is cheap
- you're just moving the problem to disk
I'm aware of most of this with kvm and libvirt. Nova doesn't expose every feature.
Nova(libvirt?) can live migrate root block devices now too.
Live snapshot works by using libvirt to mirror the qcow2 device. 

Database migrations
-------------------
They use sqlalchemy
They test on every commit
Commit » gerrit » zuul » turbo hipster » gerrit
They test upgrades from previous versions and downgrades from the latest patch.
They capture counters between upgrades of each migration
They test with inside containers
Percona is faster than mysql, at least at migrations
Limit 60 seconds on migrations
They use shadow tables for downgrades
Something about running Tempest against resulting data. 

Vagrant Rackspace
-----------------
http://thornelabs.net/2013/12/17/deploy-rackspace-private-cloud-entirely-within-a-vagrantfile-on-virtualbox-or-vmware-fusion.html
Local demo, need to do
They use chef
Guy started 9 months ago with openstack
Ssh-keyscan $ip > known_hosts
He's really proud of his vagrantfile. 

Keynote
-------
From yesterday:
Openstack CI destroys after tests and log gathering.

Move fast.
Average company tenure 1960: 61 years, now: 18.
75% of the S&P 500 will be replaced by 2021?
Telco business is #1 global revenue
AT&T guy: Toby Ford
- "AT&T basically invented the waterfall method."
- Asterisk, Defcore, refstack, mentioned
Sony guy: Joel Johnston
- most dramatic baseball game ad ever
- uses openstack to manage the entire" online" aspect of these games
DigitalFilm Tree
- between two firms
- Sweaters as a Service
- he can't just hire an openstack guy, it's still too specialized.
SolidFire: Dave Wright
- started in atlanta
- siloed model of datacenters is dead.
- the data center is now one big computer, openstack is the OS
Shuttleworth
- Pushing Juju
- landscape has Openstack support
- Metal as a Service
- flashy demos
- Ubuntu.com/jumpstart $10k, 2 weeks
- 14,04 has lxc 1.0
- Plastic as a service

Distros
-------
Distros vs Products
Pick a reference architecture
Watch out for nested virtualization
All HA models are slightly different, nova, neutron, cinder, etc
Community is so big, you HAVE to upgrade every 6 months
Watch for nonincluded support, and paid upgrades
Review Mirantis Drivelog, Openstack Marketplace
Closer to trunk, better chance for fixes
How are issues with your product handled? 

Containers
----------
Thinks they're the next big thing
1% to 3% bare metal speed
Geard, parallels for orchestration
migration via criu project
Used dstat to gather metrics
His deck is on slideshare, boden russell

Getting Started
---------------
They're using RDO
Trystack uses Facebook, but is a free "donated" trial of openstack
The talk is recorded, really need to rewatch
All users have to be authenticated and belong to a tenant.
'services' tenant is for general purpose for cluster management.
Search for them on slideshare
Radez.fedorapeople.org

CI&D
----
Fluo from ebay
Uses Gerrit to enforce change review.
Uses commit number + time in seconds for build version
Uses git tag as package version
DEFINE A VERSIONING STANDARD

Devops Tools
------------
Recommends not chasing trunk, using one release back
He's had best luck with packer, then clonehd | qemu-img convert
He uses a lot of rundeck
"Reprovision, don't repair. Servers are cattle, not pets. Don't chase unicorns"
Use Tempest on your staging cloud. 


