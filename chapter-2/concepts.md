#### Fundamental Concepts

Before running our first container let us understand some of the key concepts
and taxonomy of container world.

* **Image**: An image is a _filesystem_ to use at runtime. It doesn't have state and is _immutable._
* **Layer**: A layer is set of changes to files. An image is composed of layers.
* **Container**: A container is a _running instance of an image_. 
* **Docker Engine**: Software platform to build, run, manage and orchestrate
  containers. It's a client-server application.
  * Docker Daemon: Daemon is a long running process for managing Docker.
  * Docker Client: Client is command-line program which communicates with Docker
    Daemon to perform actions on images, containers etc.
