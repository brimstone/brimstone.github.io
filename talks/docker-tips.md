Docker Tips & Tricks
====================
Matt

[@brimston3](https://twitter.com/brimston3)

https://brimstone.github.io

Note: <a href="slides.html?talks/docker-tips.md#!">View this as slides</a>



Play With Docker
----------------
No need to install anything!

http://play-with-docker.com



CLI: Cleaning up
----------------
Containers:
```
$ docker ps -a -q -f status=exited | xargs docker rm -v
```

Images:
```
$ docker images -q -f dangling=true | xargs docker rmi
```

Volumes:
```
$ docker volume ls -q -f dangling=true | xargs docker volume rm
```

docker >= 1.13:
```
$ docker system prune
```

Note: Save some space on your disk!
This doesn't work for docker for mac/win. You need to actually rebuild the VM
for that.


CLI: Stay clean
---------------
When starting containers:
```
$ docker run --rm
```

When removing a container:
```
$ docker rm -v $containerid
```

Note: Often don't use `-v` to remove volumes too!


CLI: Container IDs
------------------

IDs can be shorted, if unique:
```
CONTAINER ID  IMAGE       COMMAND   CREATED     STATUS    NAMES
3f263913ff25  brimstone/… "/loader" 2 secs ago  Up 1 sec  suspicious_noyce
9620b52c84ba  brimstone/… "/loader" 15 secs ago Up 14 sec gloomy_bhaskara
```

```
$ docker rm -vf 3f
```

```
$ docker inspect 9
```

Note: You don't have to use the full ID in cli commands, just use enough it's
unique.


CLI: `-f`
---------
- force (danger!):
  - `rm`
- filter:
  - `ps` (also has `--format`)
- format:
  - `inspect`
-- `volume ls`
  - `volume inspect`


CLI: `--format`
---------------
```
$ docker inspect -f '{{json .Config.Labels}}' brimstone/kali | jq
{
  "org.label-schema.build-date": "",
  "org.label-schema.schema-version": "1.0.0-rc1",
  "org.label-schema.vcs-ref": "",
  "org.label-schema.vcs-url": "https://github.com/brimstone/docker-kali"
}
```

```
$ docker inspect --format '{{json .Config.Env}}' nginx | jq
[
  "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
  "NGINX_VERSION=1.11.8-1~jessie"
]
```

More about jq: https://stedolan.github.io/jq/

More about labels: http://label-schema.org


CLI: Simple dashboard
---------------------
```
watch -n 2 'docker ps --format "table {{.ID}}\t {{.Image}}\t {{.Status}}"'
```



CLI: history
------------
```
$ docker history nginx --no-trunc
```



Images: nsenter
---------------
Enter mount namespace of the host:
```
$ docker run --rm -it --privileged --pid=host \
    fedora nsenter -t 1 -m -u -i -n sh
```

Enter namespaces of any container:
```
$ docker run --rm -it --privileged --pid=container:redis \
    fedora nsenter -t 1 -m -u -i -n sh
```
A bit less dramatic:
```
$ docker exec -it -u 0:0 redis sh
```


Multi arch!
-----------

- makes `docker pull user/image:latest` become
  - on laptop: `docker pull user/image:amd64`
  - on raspi: `docker pull user/image:arm`
- https://github.com/estesp/manifest-tool



Label-Schema & Microbadger
--------------------------
- [label-schema](http://label-schema.org/rc1/)
- [Dockerfile](https://github.com/brimstone/docker-kali/blob/master/Dockerfile#L7-L10)
- [hooks/build](https://github.com/brimstone/docker-kali/blob/master/hooks/build)
- [on Microbadger](https://microbadger.com/images/brimstone/kali)



Resources
---------
- https://codefresh.io/blog/everyday-hacks-docker/

