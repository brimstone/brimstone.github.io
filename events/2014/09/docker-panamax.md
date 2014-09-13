Docker Meetup: Panamax
----------------------
######Wed Sep 10 18:40:03 EDT 2014

 * [panamax.io](http://panamax.io)
 * [@rupakg](https://twitter.com/rupakg)
 * Product of Centurylink
 * Uses Vagrant for now
 * Really wants to run on CoreOS
 * Slides on [speakerdeck](https://speakerdeck.com/rupakg/atl-docker-meetup-showcasing-panamax)

```
# still needs fleet and etcd
docker run --name PMX_API -d -v /var/run/docker.sock:/var/run/docker.sock centurylink/panamax-api

docker run --name PMX_UI --link PMX_API:PMX_API -d -p 3000:3000 centurylink/panamax-ui
```
