#### Ubuntu

[https://docs.docker.com/engine/installation/linux/ubuntu/\#install-using-the-repository](https://docs.docker.com/engine/installation/linux/ubuntu/#install-using-the-repository)

```
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

$ sudo apt-get update

$ sudo apt-get install docker-ce
```

#### Verify Installation

```
$ docker -v

Docker version 17.03.0-ce, build 3a232c8
```



