#### Multiple versions of MySQL Containers

Let us move onto see how Docker facilitates running different versions of same
application on same host with full isolation suport.

We had downloaded MySQL version 5.7.4 in previous exercise. Pull version 5.5
now.

```
$ docker pull mysql:5.5
5.5: Pulling from library/mysql
...
...
Status: Downloaded newer image for mysql:5.5
```

Run this container as your ran the previous one. Change container name and image
name accordingly. You should be able to see two versions of MySQL running in
`docker ps`.

```
docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
24ec6de84ca6        mysql:5.5           "docker-entrypoint..."   3 seconds ago       Up 2 seconds        3306/tcp            mysql55
43f8896cd9b1        mysql:5.7.4         "/entrypoint.sh my..."   13 minutes ago      Up 13 minutes       3306/tcp            mysql57

$ docker exec mysql57 mysql --version
mysql  Ver 14.14 Distrib 5.7.4-m14, for linux-glibc2.5 (x86_64) using  EditLine wrapper

$ docker exec mysql55 mysql --version
mysql  Ver 14.14 Distrib 5.5.54, for linux2.6 (x86_64) using readline 5.1
```

There you it, running multiple versions of MySQL with full app isolation.

Just think about for a moment, if container images are immutable, what will
happen to the data that you have inserted when container is killed and removed? 
