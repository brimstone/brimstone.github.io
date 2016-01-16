Truly Static Binaries with Go
-----------------------------
Matt

@brimston3

http://brimstone.github.com

Note: - Who knows go builds static binaries?
- Who has used cgo?
- Who has used docker?



History
-------


Hub.docker.com
--------------

![](musl-go/hub.docker.com.png)

Note: - Who's setup a Automated Build on the Docker hub?
- Link to GitHub repo
- `git push` -> `docker pull`


Dockerfile
----------
```
FROM golang:onbuild
```

Note: container for this, super cool


```
$ docker build …
Sending build context to Docker daemon 164.4 kB
Step 1 : FROM golang:onbuild
onbuild: Pulling from library/golang
…
# Executing 3 build triggers...
Step 1 : COPY . /go/src/app
Step 1 : RUN go-wrapper download
 ---> Running in 8c8e5fa8b404
+ exec go get -v -d
Step 1 : RUN go-wrapper install
 ---> Running in d2f233c4c5aa
+ exec go install -v
app
 ---> 19d1e224608d
```

Note: downside: bring everything with you


Results
-------
```
REPOSITORY  TAG      IMAGE ID      CREATED      VIRTUAL SIZE
golang      onbuild  6b10dfd0c832  2 days ago   725.1 MB
helloworld  latest   19d1e224608d  2 hours ago  727.5 MB
```
Note: !!!


There has to be a better way
----------------------------
![](musl-go/has.to.be.a.better.way.gif)

Note: This is an easter egg for those of you reading along ;)


Travis-ci
---------
![](musl-go/travis-ci.png)

Note: - searching around, other projects seem to use travis-ci
- looks like it'll give me the same work flow, `git push` -> `docker pull`


Test Project
------------
http://github.com/brimstone/docker-static

![](musl-go/github.docker-static.png)

Note: so I made a project to test this out and investigate if this was possible


main.go
-------
```
package main

import "log"

func main() {
	log.Println("hello world!")
}
```

Note: could be made simpler with println()


.travis.yml
-----------
```
language: go

sudo: required
services:
 -  docker

script:
  - make
```

Note: sudo: isn't required, actually


Makefile
--------
```
.PHONY: all build docker-image docker-push

all: build docker-image docker-push

build:
	go get -v -d
	CGO_ENABLED=0 go build -a -installsuffix cgo -ldflags '-s' -o main

docker-image:
	docker build -t brimstone/static .

docker-push:
	@[ -f ${HOME}/.dockercfg ] || docker login -e="${DOCKER_EMAIL}" \
		-u="${DOCKER_USERNAME}" -p="${DOCKER_PASSWORD}"
	docker push brimstone/static
```

Note: - Walk through each target really fast
- Mention hidden secrets


Dockerfile
----------
```
FROM scratch

CMD []
ENTRYPOINT ["/main"]

ADD main /
```

Note: Dockerfile is now 4 lines instead of 1


Result
------
```
❯ ls -lh main
-rwxr-xr-x 1 brimstone brimstone 1.6M Jan 16 12:29 main*
```
```
REPOSITORY        TAG      IMAGE ID      CREATED        VIRTUAL SIZE
brimstone/static  latest   a1d5db3d5851  13 seconds ago 1.672 MB
```

Note: - success!
- Now you have the history



Original Goal
-------------
![](musl-go/nomadproject.io.png)

Note: - swarm + compose at work is lacking
- like everything else made by hashicorp except vagrant, it's written in go
- take the same route


Dragons
-------
```
2016/01/16 20:26:55 [DEBUG] client: updated allocations at index 8 (1 
allocs)
2016/01/16 20:26:55 [DEBUG] client: allocs: (added 1) (removed 0) (upd
ated 0) (ignore 0)
2016/01/16 20:26:55 [DEBUG] client: starting runner for alloc '2ad66df
f-b902-f359-f2c1-bb434704b155'
2016/01/16 20:26:55 [WARN] client: failed to build task directories: u
ser: lookup username nobody: no such file or directory
2016/01/16 20:26:55 [DEBUG] client: updated allocations at index 10 (1
 allocs)
2016/01/16 20:26:55 [DEBUG] client: allocs: (added 0) (removed 0) (upd
ated 1) (ignore 0)
```

Note: - Almost, but no cigar
- Why? to drop privileges for security
- Should be easy enough to debug right?



Rabbit hole
-----------
![](musl-go/rabbit.hole.gif)

Note: this should have been a red flag


user.Lookup()
-------------
```
…
if lookupByName {
	nameC := C.CString(username)
	defer C.free(unsafe.Pointer(nameC))
	// mygetpwnam_r is a wrapper around getpwnam_r to avoid
	// passing a size_t to getpwnam_r, because for unknown
	// reasons passing a size_t to getpwnam_r doesn't work on
	// Solaris.
	rv = C.mygetpwnam_r(nameC,
		&pwd,
		(*C.char)(buf),
		C.size_t(bufSize),
		&result)
	if rv != 0 {
		return nil, fmt.Errorf("user: lookup username %s: %s", usern…
…
```

Note: Because of this code, I can't disable cgo


Can I just short it?
--------------------
https://en.wikipedia.org/wiki/Userid#Special_values

Linux: 2^16−2 = 65,534

OpenBSD: 2^15-1 = 32,767

Note: no


getpwnam
--------
```
#include <pwd.h>
#include <stdio.h>

int main( void )
{
        struct passwd *pwd = getpwnam( "nobody" );

        if (pwd) {
                printf( "uid is: %d\n", pwd->pw_uid );
				return 0;
		}
        else{
                printf( "error\n" );
				return 1;
		}
}
```

Note: - stole this from someone online.
- object to compile it statically, just to see what's up


getpwnam
--------
> getpwnam.c:(.text+0xe): warning: Using 'getpwnam' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking

Note: should have been second red flag


strace
------
```
open("/etc/nsswitch.conf", O_RDONLY|O_CLOEXEC) = 3
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libnss_compat.so.2", O_RDONLY|O_CLOEXEC) …
open("/lib/x86_64-linux-gnu/libnsl.so.1", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/ld-linux-x86-64.so.2", O_RDONLY|O_CLOEXEC…
open("/etc/nsswitch.conf", O_RDONLY|O_CLOEXEC) = 3
open("/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libnss_nis.so.2", O_RDONLY|O_CLOEXEC) = 3
open("/lib/x86_64-linux-gnu/libnss_files.so.2", O_RDONLY|O_CLOEXEC) =…
open("/etc/passwd", O_RDONLY|O_CLOEXEC) = 3
uid is: 65534
+++ exited with 0 +++
```

Note: shout out to my homie libnss!


Alternative route
-----------------

- Run as not uid 0
- can't open /var/run/docker.sock

Note: owner is root, group is docker, 128


Alternative route 2
-------------------

- Wrapper script
- check `$DOCKER_HOST` for unix:// prefix
- stat /var/run/docker.sock
- make /data directory owned by this user
- change to this account

Note: maintenance nightmare


![](musl-go/maintenance.nightmare.jpg)

Note: amirite?



altroute3 best altroute
-----------------------

Note: ask who's used a different libc?


musl
----

TODO screenshot of musl's website
