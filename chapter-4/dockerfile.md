#### Create Dockerfile

Start with creating a Dockerfile inside your working directory.

```
FROM php:7.0-apache
COPY src/ /var/www/html/
```

#### Add php source

```
$ mkdir src
$ echo "<? phpinfo(); ?>" > src/index.php
```

#### Build Image

```
$ docker build -t php-local .

Sending build context to Docker daemon 3.584 kB
Step 1/2 : FROM php:7.0-apache
 ---> 21723f8dfdac
Step 2/2 : COPY src/ /var/www/html/
 ---> Using cache
 ---> 295948c0127a
Successfully built 295948c0127a
```

The `-t` argument is for tagging your image. This tag is used while running a container from the image.

Notice that the number of Steps involved in building an image is exactly equal to the number of commands in our Dockerfile. Each command is executed and committed as a layer in docker file system. You can

#### Run Container

```
docker run -d -p 8080:80 --name my-app php-local
```

Open [http://localhost:8080/](http://localhost:8080/ "localhost:8080") in your browser to verify if phpinfo is being served.

#### Check logs

```
docker logs -f my-app
```

#### Cleanup

```
docker stop my-app && docker rm my-app
```

---

###### https://hub.docker.com/\_/php/



