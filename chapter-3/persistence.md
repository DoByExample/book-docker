#### Persisting Data using Volumes

In the closure of previous exercise we learned that the any newly generated data  
which is not part of docker images will get lost. This is not an acceptable  
solution in case DBs where we have to keep the Data Highly Available.

So to enable storing of the Data in persistent manner Docker has an option of  
mounting a host volume inside container. This way whatever Data that is getting  
writtent to will directly go to host volume and will be persisted there.

e.g. To start MySQL wherein you want to keep its DB files in presistence on disk  
you issue following command.

```
mkdir -p ~/Docker/docker101
docker run --name mysql57 -d -e MYSQL_ROOT_PASSWORD=root -v /Users/nixmaniack/docker101/mysql:/var/lib/mysql mysql:5.7.4
```

Here `-v` parameter tells `docker run` command to mount the host volume  
`~/docker101/mysql` inside container on `/var/lib/mysql` path. Since MySQL  
writes its DB files in `/var/lib/mysql` all the data that's generated will be  
saved on disk. So in case MySQL container isn't performing optimally, you should  
be able to kill current one and start new with existing data.

You can check host path that you have given for the files that MySQL has  
created.

```
$ ls -l ~/docker101/mysql
total 110596
-rw-rw----  1 nixmaniack staff       56 Mar 19 04:19 auto.cnf
-rw-rw----  1 nixmaniack staff 50331648 Mar 19 04:23 ib_logfile0
-rw-rw----  1 nixmaniack staff 50331648 Mar 19 04:19 ib_logfile1
-rw-rw----  1 nixmaniack staff 12582912 Mar 19 04:23 ibdata1
drwx------ 81 nixmaniack staff     2754 Mar 19 04:19 mysql
drwx------ 78 nixmaniack staff     2652 Mar 19 04:19 performance_schema
drwx------  5 nixmaniack staff      170 Mar 19 04:20 test
```



