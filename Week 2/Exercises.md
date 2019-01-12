# Week 2

## Exercise 2.1

docker-compose file:

```
version: '3'

services:

    backend:
      image: backend-example
      build: .
      ports:
        - 8000:8000

    frontend:
      image: frontend-example
      build: ../frontend-example-docker/
      ports:
        - 5000:5000
```

## Exercise 2.2

- docker-compose file:

```
version: '3'

services:

    backend:
      image: backend-example
      build: .
      ports:
        - 8000:8000
      environment:
        REDIS: redis

    frontend:
      image: frontend-example
      build: ../frontend-example-docker/
      ports:
        - 5000:5000

    redis:
      image: redis
```

## Exercise 2.3

- docker-compose file:

```
version: '3'

services:

    backend:
      image: backend-example
      build: ../backend-example-docker/
      ports:
        - 8000:8000
      environment:
        DB_USERNAME: postgres
        DB_PASSWORD: sekret
        DB_HOST: db

    frontend:
      image: frontend-example
      build: ../frontend-example-docker/
      ports:
        - 5000:5000

    db:
      image: postgres
      restart: always
      environment:
        POSTGRES_PASSWORD: sekret
```

## Exercise 2.4

- docker-compose file:

```
version: '3'

services:

    backend:
      image: ml-kurkkumopo-backend
      build: ml-kurkkumopo-backend/
      ports:
        - 5000:5000
      volumes:
        - model:/src/model

    frontend:
      image: ml-kurkkumopo-frontend
      build: ml-kurkkumopo-frontend/
      ports:
        - 3000:3000

    training:
      image: ml-kurkkumopo-training
      build: ml-kurkkumopo-training/
      volumes:
        - images:/src/imgs
        - data:/data
        - model:/src/model

volumes:
  model:
  images:
  data:
```

## Exercise 2.6

- docker-compose file:

```
version: '3'

services:

    backend:
      image: backend-example
      build: ../backend-example-docker/
      ports:
        - 8000:8000
      environment:
        DB_USERNAME: postgres
        DB_PASSWORD: sekret
        DB_HOST: db
        REDIS: redis

    frontend:
      image: frontend-example
      build: ../frontend-example-docker/
      ports:
        - 5000:5000

    db:
      image: postgres
      restart: always
      environment:
        POSTGRES_PASSWORD: sekret
      volumes:
        - postgres-data:/var/lib/postgres/data

    redis:
      image: redis
      command: ["redis-server", "--appendonly", "yes"]
      volumes:
        - redis-data:/data

volumes:
  redis-data:
  postgres-data:
```
