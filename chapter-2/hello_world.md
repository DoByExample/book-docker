#### Running a hello-world container

At this point, we have enough understanding of components involved in Docker.
Let us start with ensuring that Docker is installed correctly and functioning
properly.

Execute `docker info` on terminal and check output:

```
$ docker info
Containers: 3
 Running: 0
 Paused: 0
 Stopped: 3
Images: 46
Server Version: 1.13.0-rc4
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host ipvlan macvlan null overlay
 ...
```

The output of `docker info` shows summary of containers, images present locally
and other information about running docker instance.

Now let's run our first container.


```
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```

If you get `Hello from Docker!` in the output, you have succesfully created a
Docker container.

