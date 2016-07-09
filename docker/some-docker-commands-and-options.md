# Docker commands and options

From [post](http://www.dwmkerr.com/learn-docker-by-building-a-microservice/).

Run an (interactive) environment is easy:

```bash
$ docker run -it haskell
$ docker run -it java
$ docker run -it python
```

Create a MySQL database server in Docker:

```bash
$ docker run --name db -d -e MYSQL_ROOT_PASSWORD=123 -p 3306:3306 mysql:latest
```

