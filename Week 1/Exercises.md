# Week 1

## Exercise 1.1

```
$ docker ps -a

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
9d8faea87114        redis               "docker-entrypoint.s…"   3 minutes ago       Exited (0) 3 seconds ago                       musing_cray
a26426403f89        mongo               "docker-entrypoint.s…"   10 minutes ago      Exited (0) 3 seconds ago                       trusting_goldstine
60b1997fee01        nginx               "nginx -g 'daemon of…"   13 minutes ago      Up 13 minutes              80/tcp              tender_nightingale

```

## Exercise 1.2

```
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED        SIZE


docker ps -a

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

## Exercise 1.3

Command to start container:

`docker run -d -it --name curl ubuntu:16.04 sh -c 'read website; sleep 3; curl http://$website;'`

Commands to install curl in the container:

`docker exec -it curl bash`

```
apt-get update
apt-get install curl
```

## Exercise 1.4

- Dockerfile:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
CMD read website; sleep 3; curl http://$website;
```

- Command to run container: `docker run -it curler`

## Exercise 1.5

- Dockerfile:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN npm install
EXPOSE 5000
CMD ["npm", "start"]
```

- Command to run container: `docker run -p 5000:5000 frontend-example`

## Exercise 1.6

- Dockerfile:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN npm install
EXPOSE 8000
CMD ["npm", "start"]
```

- Command to run container `docker run -p 8000:8000 backend-example`

## Exercise 1.7

- Front-end dockerfile:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN npm install
EXPOSE 5000
ENV API_URL="http://localhost:8000/"
CMD ["npm", "start"]
```

- Backend dockerfile:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN npm install
EXPOSE 8000
ENV FRONT_URL="http://localhost:5000"
CMD ["npm", "start"]
```

- Command to run front-end container: `docker run -d -p 5000:5000 frontend-example`
- Command to run backend container: `docker run -d -p 8000:8000 backend-example`

## Exercise 1.8

- Link to [DockerHub repo](https://cloud.docker.com/repository/docker/mavai/hello_world_react)
