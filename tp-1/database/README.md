### Database
[Back](../README.md)
#### Basics
Using the given `Dockerfile`, i run
```sh
$ docker build ./tp-1/database/ -t tp1-part01

$ docker run -p 5432:5432 --name tp1-part01-ex1 tp1-part01
```
Running with a network:
``` sh
$ docker network create app-network

$ docker run --network app-network -p 5432:5432 --name tp1-part01-ex2 -d tp1-part01

$ docker run --network app-network -p 8090:8080 --name tp1-part01-ex3 -d adminer

```
For adminer: the url should be from the container, so we use `tp1-part01-ex2:5432`

#### Init Database
Added a line to `Dockerfile`
```Dockerfile
COPY setup-db /docker-entrypoint-initdb.d/
```

```sh
$ docker build ./tp-1/database/ -t tp1-part01

$ docker run -p 5432:5432 --name tp1-part01-ex4 --network app-network -d tp1-part01
```

#### Persist data
```sh
$ docker build ./tp-1/database/ -t tp1-part01
$ docker run --network app-network -p 8090:8080 --name tp1-part01-ex5 -d --rm adminer
$ docker run -p 5432:5432 --name tp1-part01-ex6 --network app-network -v ./pg-data:/var/lib/postgresql/data -d --rm tp1-part01
```
*Note: on Windows, use `.\pg-data` instead of `./pg-data`*