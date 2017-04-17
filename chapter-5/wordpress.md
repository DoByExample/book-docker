**Compose** is a tool for defining and running multi-container Docker applications. With Compose, you use a Compose file to configure your application’s services. Then, using a single command, you create and start all the services from your configuration.

Using Compose is basically a three-step process.

1. **Define your app’s environment** with a Dockerfile so it can be reproduced anywhere. \(Not needed if you are using public images\)

2. **Define the services** that make up your app in docker-compose.yml so they can be **run together in an isolated environment**.

3. Lastly, **run docker-compose up** and Compose will start and run your entire application.

---

##### Create the compose file

Create a _docker-compose.yml_ file inside your working directory and define services for PHP and MySQL as shown below.

```yaml
version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: wordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:
```

##### Building the environment

`docker-compose up -d`

##### Cleanup

`docker-compose down`

---

[https://docs.docker.com/compose/overview/](https://docs.docker.com/compose/overview/)

