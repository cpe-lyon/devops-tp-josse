### Http Server
[Back](../README.md)
#### Choose an appropriate base image
```sh
$ docker network create tp1-http-net

$ docker build -t tp1-backend-pg ./tp-1/database/
$ docker build -t tp1-backend-http ./tp-1/backend-api/simple-api-student-main
$ docker build -t tp1-http ./tp-1/http-server

$ docker run --network tp1-http-net --name tp1-backend-db -v ./backend-data:/var/lib/postgresql/data -d --rm tp1-backend-pg
$ docker run --network tp1-http-net -p 8090:8080 --name tp1-backend-adm -d --rm adminer
$ docker run --network tp1-http-net --name tp1-backend-srv -d --rm tp1-backend-http
$ docker run --network tp1-http-net --name tp1-http-index -p 80:80 tp1-http
```