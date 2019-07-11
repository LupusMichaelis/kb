# Docker Daemon

Enable Uset NS remap:

```sh
cat > /etc/docker/daemon.json
{
  "userns-remap": "testuser"
}
```
## Monitoring

```sh
ctop
```

# Docker use

[Cheat sheet](https://github.com/wsargent/docker-cheat-sheet)

Docker daemon stores stuff in ```/var/lib/docker/```.

```sh
# Add yourself to docker group, so you can play as you like it!
addgroup $USER docker

# Status commands
systemctl status docker
docker ps				# List containers
docker network ls
docker volume ls
docker-composer ps

docker rm $(docker ps -qa --filter='Status=exited')

# Prefetch images of Linux distributions
docker pull archlinux/base
docker pull fedora
docker pull alpine
docker pull debian

docker run -it alpine sh # Interactive instance
docker run -dt alpine sh # Daemonized instance

# Clean exited dockers
docker rm $(docker ps -aq -f status=exited)

# Clean up Joffrey style:
mids=$(docker ps -q); docker stop $mids; docker rm $mids

# Recover an exited Docker container:
docker attach $(docker start $did)

# Building
docker build . # Dockerfile in cwd
docker build -f /path/to/a/Dockerfile .

# Alternatively, you can commit and use the commited image
docker commit $did $image
docker run -it $image sh
```

docker inspect --format '{{ .NetworkSettings.IPAddress }}' $instance
docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $instance
docker inspect --format '{{ .NetworkSettings.Networks.'"$network_name"'.IPAddress }}' $instance

## Communications with container

```sh
# send HUP signal to named container
docker kill --signal=HUP $cname
```

Root access to running container:

```sh
docker exec -it -u root $cid bash
```

## Compositing

docker-compose build web # Build one container image
docker-compose build	 # Build all container images referenced in docker composer file

docker-compose run -d web

## WTF

CMD "my-cmd args" # We'll be seen as a command with no arguments (space is part of command name
ENV/ARGS: images building ignores ENV variables, have to use ARG in Dockerfile

Beware of the difference between system and exec invokation of CMD and ENTRYPOINT.

Read the best practice [guidelines](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/),
as it states various traps you will fall into (especially those concerning image caching).

Rogue package managing tools like Pear, npm, yarn and PHP Composer, are compiled against glibc, which
prevents them to run in a system where a different libc is provided, like Archlinux, Busybox and Alpine.
It is an [opened issue](https://github.com/nodejs/build/issues/1140) for NodeJS.

## Misc

When you mount a volume, docker protects against suid bombs (an exe with suid bit on will not run, and perms
updated upon copy.

```sh
docker run -it -v $PWD/toto:/toto alpine sh
cd /toto
apk update && apk add clang apk-sdk
cat > venom.c
```

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main()
{
        printf("UID: %u\n", getuid());
}
```

```sh
clang venom.c -o venom
chmod +x,u=rxs venom
```

From host:

```term
$ cd toto
$ ls -l venom
-r-sr-xr-x 1 root root 10712 Jan  8 09:15 venom
$ ./venom
$ cp venom /tmp
$ ls -l /tmp/venom
-r-xr-xr-x 1 mickael mickael 10712 Jan  8 09:25 /tmp/venom

```
<<<<<<< HEAD
# Debian

```ps``` is provided by ```procps``` package.

# Alpine

## Package management

apk search $pkgname
apk add $pkgname

## Configuration and stuff

Configuration tools are in a package that is not installed by default.

```sh
apk add alpine-conf
setup-timezone -z Europe/Paris
```

## App host

apk add apache2-php5
apk add php5-mysqli

## DB host

apk add mariadb mariadb-server-utils

## Symphony host

apk add php5 # For CLI composer tools
<!-- TODO: persistent volume -->

## Native dev machine

apk add clang alpine-sdk build-base git vim

# Traps

## UID

An issue while building images, is to map the docker UID to an existing UID, and
especially to the user's UID. If most people are using the first non-privileged user
created in their system, `1000:1000`, it not the case for everyone.

So you could be tempted to use ${UID} in your Dockerfile or Docker Compose file, to set up
the UID/GID. Unfortunatelly, those are shell variables, and will not be readily avialable
in your configuration files.

A trick is to make it available before running any build or run :

```sh
export UID
export GID
```
