# Week 1

## Exercise 1.1

```
$ docker ps -a

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
9d8faea87114        redis               "docker-entrypoint.s…"   3 minutes ago       Exited (0) 3 seconds ago                       musing_cray
a26426403f89        mongo               "docker-entrypoint.s…"   10 minutes ago      Exited (0) 3 seconds ago                       trusting_goldstine
60b1997fee01        nginx               "nginx -g 'daemon of…"   13 minutes ago      Up 13 minutes              80/tcp              tender_nightingale

```

## Exercise 2

```
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED        SIZE


docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## Exercise 3

Command to start container:

`docker run -d -it --name curl ubuntu:16.04 sh -c 'read website; sleep 3; curl http://$website;'`

Commands to install curl in the container:

`docker exec -it curl bash`

```
apt-get update
apt-get install curl
```

## Exercise 4

- Dockerfile [HERE](exercise_4/Dockerfile)
- Command to run container: `docker run -it curler`
