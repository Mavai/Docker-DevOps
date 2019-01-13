# Week 3

## Exercise 3.1

Sizes before optimization:

```
backend-example           latest                9deb5a76925f        15 hours ago        344MB
frontend-example          latest                4349074fd260        15 hours ago        441MB
```

Sizes after optimization:

```
backend-example           latest                c13c2a066652        4 seconds ago       316MB
fronted-example           latest                6c91ca373a23        7 minutes ago       438MB
```

Optimized dockerfiles:

```
FROM ubuntu:16.04

ENV FRONT_URL="http://localhost:5000"

COPY . .
RUN apt-get update && apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt install -y nodejs && \
    npm install && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8000

CMD ["npm", "start"]
```

```

FROM ubuntu:16.04

ENV API_URL="http://localhost:8000"

COPY . .
RUN apt-get update && apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_10.x | bash &&\
    apt install -y nodejs &&\
    npm install && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/lists/*

EXPOSE 5000

CMD ["npm", "start"]
```

## Exercise 3.2

Dockerfile:

```
FROM ubuntu:16.04

WORKDIR /app

RUN apt-get update && \
apt-get install -y python python-pip python-dev python-setuptools wget ffmpeg && \
pip install -U pip setuptools yle-dl

ENTRYPOINT ["yle-dl"]
```

## Exercise 3.3

Dockerfiles:

```
FROM ubuntu:16.04

ENV API_URL="http://localhost:8000"

COPY . .
RUN apt-get update && apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_10.x | bash &&\
    apt install -y nodejs &&\
    npm install && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/lists/* && \
    useradd -m app

USER app

EXPOSE 5000

CMD ["npm", "start"]
```

```
FROM ubuntu:16.04

ENV FRONT_URL="http://localhost:5000"

COPY . .
RUN apt-get update && apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt install -y nodejs && \
    npm install && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/apt/lists/* && \
    useradd -m app

USER app

EXPOSE 8000

CMD ["npm", "start"]
```

## Exercise 3.4

Sizes before changes:

```
backend-example           latest                c13c2a066652        4 seconds ago       316MB
fronted-example           latest                6c91ca373a23        7 minutes ago       438MB
```

Sizes after changes:

```
backend                   latest                bc1c19ff79b0        55 seconds ago       130MB
frontend                   latest                2a9f83e2b6aa        4 minutes ago        227MB
```

Dockerfiles:

```

FROM node:alpine
WORKDIR /node
ENV FRONT_URL="http://localhost:5000"

COPY . .
RUN npm install && \
 chmod -R 777 /node

USER node

EXPOSE 8000

CMD ["npm", "start"]

```

```

FROM node:alpine
WORKDIR /node
ENV API_URL="http://localhost:8000"

COPY . .
RUN npm install && \
 chmod -R 777 /node
USER node

EXPOSE 5000

CMD ["npm", "start"]

```

## Exercise 3.5

Sizes before and after:

```
hello_world_react         latest                16ef0d7af83c        41 hours ago        677MB
hello-world-react         latest                df7bd702f9a7        About a minute ago   466MB

```

Dockerfile before and after:

```
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
COPY . .
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]
```

```
FROM node:alpine

WORKDIR /node
COPY . .

RUN npm install && \
    chmod -R 777 /node

EXPOSE 3000

CMD ["npm", "start"]
```

## Exercise 3.6 b.

### Benefits of Docker and when to use it

One of the main benefits of using Docker is reproducibility. All the containers built from the same image are identical and work similarly regardless of the machine, as long as it can run Docker. This way situations where the developed software only works on some machines can be avoided.

Other benefits include isolation and easy version management. When running applications with a Docker configuration, everything happens inside containers. No dependencies or settings are needed on the host computer and instead, these are installed inside the container. This way any possible dependency conflicts with the host machine are avoided. It is also easy to create different versions of the software under development by creating multiple images with different dependencies or settings. This way, for example, different versions for testing and stage environments can be easily maintained.

Docker can be useful when running multiple application on a single machine. Some of these applications may, for example, require different versions of the same dependency. When using Docker, this is not a problem because these applications would run on different containers that are totally independent so that no conflicts arise. Another use case would be for development teams. With Docker, the application under development could be run in a similar environment compared to production on the developers' machine without needing to re-configure their own environment.
