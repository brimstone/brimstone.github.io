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
nobody error
```

Note: Almost, but no cigar


Rabbit hole
-----------

- try chmod and USER
- error it can't connect to docker.sock
- Parsing $DOCKER_HOST
- Maintenance headache

