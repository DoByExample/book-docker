#### Rest Of The World Containers - Running MySQL

So far we have covered concepts of containers and how to start, stop, delete
them. Let's now see an example of running a real life application on Docker.

We will take an example of MySQL.

Go ahead and pull MySQL version 5.7.4

```
$ docker pull mysql:5.7.4
5.7.4: Pulling from library/mysql
a3ed95caeb02: Pull complete
a9816d489674: Pull complete
b1f7ef5cc072: Pull complete
c7110e7a9f56: Pull complete
d78d8ec4f800: Pull complete
52e42de90064: Pull complete
c8a5c40648db: Pull complete
c535209921b3: Pull complete
Digest: sha256:244082ec0eeb98d04bc0b7c556be0dbfa900430d651634eb946216ab91be2435
Status: Downloaded newer image for mysql:5.7.4
```

Once you have downloaded MySQL Docker Image, run it as follows to start the
Database. 

```
$ docker run --name mysql57 -d -e MYSQL_ROOT_PASSWORD=root mysql:5.7.4 
43f8896cd9b1e273f0d83f546b99173b5b09c1e2efd89577284521ee2cf97c05
```

Here we see some new options to `docker run` command.

  * `--name`: This arguments names the newly started container with given value.
    We can use this name instead of `container id` to refer to this container.
  * `-d`: To run this Database Container in the background forever, we pass `-d`
    to daemonize. 
  * `-e`: This is used to pass environment variables inside container. MySQL
    container expect MYSQL_ROOT_PASSWORD environment variable to be able to set
    root user password. 
    
  And lastly we have specified container image name with tag. 
  

Verify that the DB container is up and running and check if DB is working fine. 

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
43f8896cd9b1        mysql:5.7.4         "/entrypoint.sh my..."   19 seconds ago      Up 18 seconds       3306/tcp            mysql57
```

Get inside container and check MySQL
```
$ docker exec -ti mysql57 bash
root@43f8896cd9b1:/# mysql -uroot -proot

root@43f8896cd9b1:/usr/local/mysql# mysql -uroot -proot -qA
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.4-m14 MySQL Community Server (GPL)

Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database test;
Query OK, 1 row affected (0.00 sec)

mysql> use test
Database changed
mysql> create table ids (id int);
Query OK, 0 rows affected (0.23 sec)

mysql> insert into ids values (1), (2);
Query OK, 2 rows affected (0.06 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from ids;
+-------------+
| id          |
+-------------+
|           1 |
|           2 |
+-------------+
2 rows in set (0.00 sec)

mysql> exit
Bye
root@43f8896cd9b1:/usr/local/mysql# exit
exit
```

You are now running MySQL version 5.7.4 on your system.
