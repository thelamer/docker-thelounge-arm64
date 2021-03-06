[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://thelounge.github.io/
[hub]: https://hub.docker.com/r/lsioarmhf/thelounge-aarch64/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/thelounge`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/thelounge-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/thelounge-aarch64.svg)](https://microbadger.com/images/lsioarmhf/thelounge-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/thelounge-aarch64.svg)](http://microbadger.com/images/lsioarmhf/thelounge-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/thelounge-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/thelounge-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-thelounge)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-thelounge/)

TheLounge (a fork of shoutIRC) is a web IRC client that you host on your own server.

__What features does it have?__  
- Multiple user support
- Stays connected even when you close the browser
- Connect from multiple devices at once
- Responsive layout — works well on your smartphone
- _.. and more!_

[![theloungeirc](https://raw.githubusercontent.com/linuxserver/community-templates/master/lsiocommunity/img/shout-icon.png)][appurl]

## Usage

```
docker create \
  --name=thelounge \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \
  -p 9000:9000 \
  lsioarmhf/thelounge-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 9000` - the port(s)
* `-v /config` -
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it thelounge /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARM64 VERSION`

To log in to the application, browse to https://<hostip>:9000.

To setup user account(s)

+ edit /config/config.json changing the value `public: true,` to `public: false,`  restart the container and enter the following from the command line of the host.

+ `docker exec -it thelounge thelounge add <user>`

+ Enter a password when prompted, refresh your browser.

+ You should now be prompted for a password on the webinterface.


## Info

* Shell access whilst the container is running: `docker exec -it thelounge /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f thelounge`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' thelounge`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/thelounge-aarch64`

## Versions

+ **25.08.18:** Use global install, simplifies adding users.
+ **20.08.18:** Rebase to alpine 3.8.
+ **06.01.18:** Rebase to alpine 3.7.
+ **31.05.17:** Rebase to alpine 3.6.
+ **09.12.16:** Initial Release.
