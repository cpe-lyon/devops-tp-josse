### Backend API
[Back](../README.md)
#### Basics
Using this `Dockerfile`:
```docker
FROM openjdk:21
COPY Main.class /usr/src/Main.class
WORKDIR /usr/src/
ENTRYPOINT ["java", "Main"]
```
I run
```sh
$ docker build -t tp1-backend ./tp-1/backend-api/HelloWorld
$ docker run --name tp1-backend-ex1 --rm tp1-backend
```
#### Multistage
Trying to use multistage with HelloWorld:
```docker
FROM eclipse-temurin:17-jdk-alpine as main-builder
COPY Main.java /usr/src/Main.java
WORKDIR /usr/src
RUN javac Main.java

FROM eclipse-temurin:17-jre-alpine
COPY --from=main-builder /usr/src/Main.class /usr/src/Main.class
WORKDIR /usr/src
ENTRYPOINT ["java", "Main"]
```
```sh
$ docker build -t tp1-backend-multistage ./tp-1/backend-api/multistage
$ docker run --name tp1-backend-ex2 --rm tp1-backend-multistage
```

Having a build stage is 

With the simple API:
```sh
$ docker build -t tp1-backend-spring ./tp-1/backend-api/simpleapi
$ docker run -p 8080:8080 --name tp1-backend-ex3 tp1-backend-spring
```

Using the code from GitHub

Re-run the container from last part
```sh
$ docker network create tp1-backend-net

$ docker build -t tp1-backend-pg ./tp-1/database/
$ docker build -t tp1-backend-http ./tp-1/backend-api/simple-api-student-main

$ docker run --network tp1-backend-net --name tp1-backend-db -v ./backend-data:/var/lib/postgresql/data -d --rm tp1-backend-pg
$ docker run --network tp1-backend-net -p 8090:8080 --name tp1-backend-adm -d --rm adminer
$ docker run --network tp1-backend-net -p 8080:8080 --name tp1-backend-srv -d --rm tp1-backend-http
```