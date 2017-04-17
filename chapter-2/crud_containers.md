#### CRUD Containers

In the last exercise we ran `hello-world` container. Now let's perform some CRUD
operations on containers. 

##### Pull Image from Docker Hub

Get `ubuntu:16.04` image. 

```
$ docker pull ubuntu:16.04
16.04: Pulling from library/ubuntu
d54efb8db41d: Pull complete
f8b845f45a87: Pull complete
e8db7bf7c39f: Pull complete
9654c40e9079: Pull complete
6d9ef359eaaa: Pull complete
Digest: sha256:dd7808d8792c9841d0b460122f1acf0a2dd1f56404f8d1e56298048885e45535
Status: Downloaded newer image for ubuntu:16.04
```

Above command pulled 16.04 version of Ubuntu. If you need latest version of an
image, you can skip appending tag. 

##### Create contaier
Create container of `ubuntu:16.04`.

```
$ docker run -i -t ubuntu:16.04 /bin/bash
root@f266bfa8e6c5:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin
srv  sys  tmp  usr  var
root@f266bfa8e6c5:/# cat /etc/issue
Ubuntu 16.04.2 LTS \n \l
```

Now unlike last exercise, you have access to the shell prompt of Ubuntu instance
that you have just created. The `-i` and `-t` flags to run commmand specify that
we want to have interactive session from this running container. We have also
specified the exact version of Ubuntu that we want to download after the image
name separated by colon. The part after colon is called _tag_ of an image. 

You can take a look at all running containers with following command.

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
f266bfa8e6c5        ubuntu:16.04        "/bin/bash"         54 seconds ago      Up 53 seconds                           jovial_euclid
```

You can now use container id of the container to perform actions on container.

##### Read from container

Let's try reading a file from running container's file system.

```
$ docker exec f266bfa8e6c5 cat /etc/issue
Ubuntu 16.04.2 LTS \n \l
```

`exec` command runs the arguments passed after container id inside container. In
this case, we passed `cat /etc/issue` which gets us the content of the file
/etc/issue present inside container. 


##### Updating container (hacky way!)

As of now, you understand that image is immutable entity and container is a
running instance of an image. So what does updating a container mean? 

Updating a container simply means _creating a new image_ after making desired
changes to running container. 

Fire up an interactive prompt to running Ubuntu container and follow commands: 
```
$ docker exec -i -t f266bfa8e6c5 /bin/bash                                                                                                        [02:49:08]
root@f266bfa8e6c5:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@f266bfa8e6c5:/# echo hello > world
root@f266bfa8e6c5:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  world
root@f266bfa8e6c5:/# exit
```

You just modified a _running container_ but updating means creating new image,
so let's create an image out of this modified container. 

```
$ docker commit f266bfa8e6c5 ubuntu-updated:16.04
sha256:454745dd236524d1b9a7a64c135d06d082978f0bd8c8110bdd0f2e1c08ba4c99
```

`commit` command takes the `container id` as first paramter and second paramter
is the _new image name_

There you have updated a docker container. 

Let's run your updated version docker container with recently commited image and
verify the change exists.

```
docker run -it ubuntu-updated:16.04 /bin/bash                                                                                                   [02:58:33]
root@f7a804c684e0:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  world
root@f7a804c684e0:/# cat world
hello
root@f7a804c684e0:/# exit
```

As you can see the file `world` is present and has content `hello`.

##### Deleting(Stop and Remove) container 

To delete a container you will need an id of container or name. If container is
running, first you will have to stop it and then delete it. 

To stop a container: 
```
$ docker stop c21cd131c192
```

And to remove the container: 

```
$ docker rm c21cd131c192
```

We have just scratched the surface of actions that you can perform on container
and images. Do take a look at `docker help` to check all the commands. 
