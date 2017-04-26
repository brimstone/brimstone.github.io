Dockercon17
-----------
Matt, Ben, Drew, Randall

https://brimstone.github.io

Note: <a href="slides.html?talks/dockercon17.md#!">View this as slides</a>


General
-------

- Austin, TX
- April 18-20, 2017
- ~5,000 attendees
- ~1,000(20%) women

Note: - https://twitter.com/solomonstre/status/854692761613852674



Announcements
-------------


Moby Project
------------

![](dockercon17/moby-project-logo.png)


Docker is, and will remain, a open source product that lets you build, ship and run containers. It is staying exactly the same from a user’s perspective. Users can download Docker from the docker.com website.

Note: https://mobyproject.org/#moby-and-docker


Moby is a project which provides a “Lego set” of dozens of components, the framework for assembling them into custom container-based systems, and a place for all container enthusiasts to experiment and exchange ideas.

Note: https://mobyproject.org/#moby-and-docker


![](dockercon17/moby-project-1.jpg)

Note: https://twitter.com/solomonstre/status/855918630915133440


![](dockercon17/moby-project-2.jpg)

Note: https://twitter.com/solomonstre/status/855918630915133440


Use cases for Moby
------------------
- linuxkit VM for Hyper-V
- docker deb and rpm
- projects like RancherOS
- docker-ee builds

Note: docker-ee can include more specific `help` commands that don't make sense in -ce


Linuxkit
--------
A toolkit for building secure, portable and lean operating systems for containers.
https://github.com/linuxkit/linuxkit


Example config
--------------
```
kernel:
  image: "linuxkit/kernel:4.9.x"
  cmdline: "console=ttyS0 console=tty0 page_poison=1"
init:
  - linuxkit/init:63eed9ca7a09d2ce4c0c5e7238ac005fa44f564b
  - linuxkit/runc:b0fb122e10dbb7e4e45115177a61a3f8d68c19a9
  - linuxkit/containerd:18eaf72f3f4f9a9f29ca1951f66df701f873060b
services:
  - name: dhcpcd
    image: "linuxkit/dhcpcd:0d4012269cb142972fed8542fbdc3ff5a7b695cd"
    binds:
     - /var:/var
     - /tmp/etc:/etc
    capabilities:
     - CAP_NET_ADMIN
     - CAP_NET_BIND_SERVICE
     - CAP_NET_RAW
    net: host
  - name: redis
    image: "redis:3.0.7-alpine"
    capabilities:
     - CAP_NET_BIND_SERVICE
     - CAP_CHOWN
     - CAP_SETUID
     - CAP_SETGID
     - CAP_DAC_OVERRIDE
    net: host
outputs:
- format: kernel+initrd
```

Note: https://github.com/linuxkit/linuxkit/blob/master/examples/redis-os.yml


New Docker Features
-------------------




Talks worth watching
--------------------


Moby's cool hacks
-----------------

[Video](https://www.youtube.com/watch?v=-h2VTE9WnZs)
- New features in Play With Docker
- [Functions as a service](http://getfaas.com)

Note: - PWD is really slick
- demo http://traning.play-with-docker.com
- Faas is kinda like Lamndas + API Gateway
