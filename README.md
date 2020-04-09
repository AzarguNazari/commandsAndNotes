# Docker Commands
```
docker-compose up
docker-comose -f fileName up
docker-compose -f filename up -d
docker-compose -f filename down
docker-compose -f imagename down --remove-orphans
docker tag tageName:version
docker push tagname:version repository:version

docker build .
docker build -f path/filename .
docker build -t tagName .
docker build -t tagName:version -t takename:version .
docker build -t tagname .


docker run imageId
docker stop imageID
docker container la -a
dcoker ps
docker images
docker run
docker stop

docker exec -it image bash


docker rm
docker rmi
docker rmi -force
docker rm -f filename
docker rmi $(docker images -q) -f



```
## Dockerfile
```
  RUN echo 'We are running some of things'
  # directive=value1
  # directive=value2
  
  FROM imageName
  # directive=value
  
  
  FROM microsoft/manoserver
  COPY testFile.txt c:\\
  RUN dir c:\
  
  DOCKER build -t -t cmd .
  
  
  
  FROM busybox
ENV foo /bar
WORKDIR ${foo}   # WORKDIR /bar
ADD . $foo       # ADD . /bar
COPY \$foo /quux # COPY $foo /quux
  
  
  ENV abc=hello
ENV abc=bye def=$abc
ENV ghi=$abc
  
  FROM <image> [AS <name>]
  FROM <image>[:<tag>] [AS <name>]
  FROM <image>[@<digest>] [AS <name>]
  
  ARG  CODE_VERSION=latest
FROM base:${CODE_VERSION}
CMD  /code/run-app

FROM extras:${CODE_VERSION}
CMD  /code/run-extras
  
  
  ARG VERSION=latest
FROM busybox:$VERSION
ARG VERSION
RUN echo $VERSION > image_version

RUN /bin/bash -c 'source $HOME/.bashrc; \
echo $HOME'

RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'

FROM ubuntu
CMD echo "This is a test." | wc -

FROM ubuntu
CMD ["/usr/bin/wc","--help"]

LABEL "com.example.vendor"="ACME Incorporated"
LABEL com.example.label-with-value="foo"
LABEL version="1.0"
LABEL description="This text illustrates \
that label-values can span multiple lines."

LABEL maintainer="SvenDowideit@home.org.au"


EXPOSE <port> [<port>/<protocol>...]
EXPOSE 80/udp
EXPOSE 80/tcp
EXPOSE 80/udp

docker run -p 80:80/tcp -p 80:80/udp ...

ADD hom* /mydir/        # adds all files starting with "hom"
ADD hom?.txt /mydir/    # ? is replaced with any single character, e.g., "home.txt"

ADD test relativeDir/          # adds "test" to `WORKDIR`/relativeDir/
ADD test /absoluteDir/         # adds "test" to /absoluteDir/

ADD arr[[]0].txt /mydir/    # copy a file named "arr[0].txt" to /mydir/

ADD --chown=55:mygroup files* /somedir/
ADD --chown=bin files* /somedir/
ADD --chown=1 files* /somedir/
ADD --chown=10:11 files* /somedir/

COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"] (this form is required for paths containing whitespace)

COPY hom* /mydir/        # adds all files starting with "hom"
COPY hom?.txt /mydir/    # ? is replaced with any single character, e.g., "home.txt"
COPY test relativeDir/   # adds "test" to `WORKDIR`/relativeDir/
COPY test /absoluteDir/  # adds "test" to /absoluteDir/
COPY arr[[]0].txt /mydir/    # copy a file named "arr[0].txt" to /mydir/
COPY --chown=55:mygroup files* /somedir/
COPY --chown=bin files* /somedir/
COPY --chown=1 files* /somedir/
COPY --chown=10:11 files* /somedir/
docker run -i -t --rm -p 80:80 nginx

FROM ubuntu
ENTRYPOINT ["top", "-b"]
CMD ["-c"]

docker run -it --rm --name test  top -H

 docker exec -it test ps aux
 
 
 FROM debian:stable
RUN apt-get update && apt-get install -y --force-yes apache2
EXPOSE 80 443
VOLUME ["/var/www", "/var/log/apache2", "/etc/apache2"]
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]



#!/usr/bin/env bash
set -e

if [ "$1" = 'postgres' ]; then
    chown -R postgres "$PGDATA"

    if [ -z "$(ls -A "$PGDATA")" ]; then
        gosu postgres initdb
    fi

    exec gosu postgres "$@"
fi

exec "$@"




#!/bin/sh
# Note: I've written this using sh so it works in the busybox container too

# USE the trap if you need to also do manual cleanup after the service is stopped,
#     or need to start multiple services in the one container
trap "echo TRAPed signal" HUP INT QUIT TERM

# start service in background here
/usr/sbin/apachectl start

echo "[hit enter key to exit] or run 'docker stop <container>'"
read

# stop service and clean up here
echo "stopping apache"
/usr/sbin/apachectl stop

echo "exited $0"





docker exec -it test ps aux



FROM ubuntu
ENTRYPOINT exec top -b



docker run -it --rm --name test top

/usr/bin/time docker stop test



FROM ubuntu
ENTRYPOINT top -b
CMD --ignored-param1

docker run -it --name test top --ignored-param2

VOLUME ["/data"]

FROM ubuntu
RUN mkdir /myvol
RUN echo "hello world" > /myvol/greeting
VOLUME /myvol


USER <user>[:<group>] or
USER <UID>[:<GID>]


FROM microsoft/windowsservercore
    # Create Windows user in the container
    RUN net user /add patrick
    # Set it for subsequent commands
    USER patrick
    
    WORKDIR /path/to/workdir
    
    
    WORKDIR /a
WORKDIR b
WORKDIR c
RUN pwd


ENV DIRPATH /path
WORKDIR $DIRPATH/$DIRNAME
RUN pwd


ARG <name>[=<default value>]

FROM busybox
ARG user1
ARG buildno
...


1 FROM busybox
2 USER ${user:-some_user}
3 ARG user
4 USER $user
...

docker build --build-arg user=what_user .


FROM busybox
ARG SETTINGS
RUN ./run/setup $SETTINGS

FROM busybox
ARG SETTINGS
RUN ./run/other $SETTINGS


1 FROM ubuntu
2 ARG CONT_IMG_VER
3 ENV CONT_IMG_VER v1.0.0
4 RUN echo $CONT_IMG_VER


FROM microsoft/windowsservercore

# Executed as cmd /S /C echo default
RUN echo default

# Executed as cmd /S /C powershell -command Write-Host default
RUN powershell -command Write-Host default

# Executed as powershell -command Write-Host hello
SHELL ["powershell", "-command"]
RUN Write-Host hello

# Executed as cmd /S /C echo hello
SHELL ["cmd", "/S", "/C"]
RUN echo hello




# Firefox over VNC
#
# VERSION               0.3

FROM ubuntu

# Install vnc, xvfb in order to create a 'fake' display and firefox
RUN apt-get update && apt-get install -y x11vnc xvfb firefox
RUN mkdir ~/.vnc
# Setup a password
RUN x11vnc -storepasswd 1234 ~/.vnc/passwd
# Autostart firefox (might not be the best way, but it does the trick)
RUN bash -c 'echo "firefox" >> /.bashrc'

EXPOSE 5900
CMD    ["x11vnc", "-forever", "-usepw", "-create"]
# Multiple images example
#
# VERSION               0.1

FROM ubuntu
RUN echo foo > bar
# Will output something like ===> 907ad6c2736f

FROM ubuntu
RUN echo moo > oink
# Will output something like ===> 695d7793cbe4

# You'll now have two images, 907ad6c2736f with /bar, and 695d7793cbe4 with
# /oink.
```


# Additional Command

```
curl URL
```


## Properties

lsof -i:8080
### Code
