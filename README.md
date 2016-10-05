[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/index.php/irc/
[podcasturl]: https://www.linuxserver.io/index.php/category/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/minisatip

[![](https://images.microbadger.com/badges/image/lsioarmhf/minisatip.svg)](http://microbadger.com/images/lsioarmhf/minisatip "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/minisatip.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/minisatip.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-minisatip)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-minisatip/)
[hub]: https://hub.docker.com/r/lsioarmhf/minisatip/

Minisatip is a multi-threaded satip server version 1.2 that runs under Linux and it was tested with DVB-S, DVB-S2, DVB-T, DVB-T2, DVB-C, DVB-C2, ATSC and ISDB-T cards. [Minisatip](https://github.com/catalinii/minisatip)

[![minisatip](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/minisatip-icon.png)][minisaturl]
[minisaturl]: https://github.com/catalinii/minisatip

## Usage

```
docker create \
--name=minisatip \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 8875:8875 -p 554:554 \
-p 1900:1900/udp
--device=/dev/dvb \
lsioarmhf/minisatip
```

**Parameters**

* `-p 8875` - the port(s)
* `-p 554` - the port(s)
* `-p 1900/udp` - the port(s)
* `-v /config` -
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `--device=/dev/dvb` - for passing through Tv-cards.
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine with s6 overlay, for shell access whilst the container is running do `docker exec -it minisatip /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Best used in conjunction with [tvheadend](https://github.com/linuxserver/docker-tvheadend)

There is no setup per se, other than adding your cards for passthrough. 

You can then use your cards as DVB inputs in apps such as tvheadend.

## Info

* To monitor the logs of the container in realtime `docker logs -f minisatip`.



## Versions

+ **18.09.16:** Add support for Common Interface.
+ **11.09.16:** Add layer badges to README.
+ **06.09.16:** Add badges to README.
+ **15.08.16:** Initial Release.
