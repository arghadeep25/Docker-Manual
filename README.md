[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/1280px-Docker_%28container_engine%29_logo.svg.png">]()

# Docker Image

- Images are read-only templates containing instructions for creating a container. A Docker image creates containers to run on the Docker platform.

- An image is composed of multiple stacked layers. Images contain the code or binary, runtimes, dependencies, and other filesystem objects to run an application. The image relies on the host operating system (OS) kernel.

- Docker Images are build using a Dockerfile, a text document containing all the commands to create a Docker image. You can also pull images from a central repository called a registry, or from repositories.

- When a Docker user runs an image, it becomes one or multiple container instances. 

- Docker images are immutable, so you cannot change them once they are created. If you need to change something, create another container with your changes, then save those as another image. Or, just run your new container using an existing image as a base and change that one.

- Images themselves do not run, but you can create and run containers from a Docker image.


# Docker Container 

- A container is an isolated place where an application runs without affecting the rest of the system and without the system impacting the application. Because they are isolated, containers are well-suited for securely running software like databases or web applications that need access to sensitive resources without giving access to every user on the system.

- Since the container runs natively on Linux and shares the host machine’s kernel, it is lightweight, not using more memory than other executables. If you stop a container, it will not automatically restart unless you configure it that way. However, containers can be much more efficient than virtual machines because they don’t need the overhead of an entire operating system. They share a single kernel with other containers and boot in seconds instead of minutes.

- Container can be used for shipping purposes by integrating all the required components for an application to run. This avoids the friction between other developers. 


# Docker Image vs Docker Container 


| Docker Image | Docker Container |
|     :---:        |     :---:      |
|Blueprint of the Container.| Instance of the Image.|
| Image is a logical entity.| Container is a real world entity.|
| Images are immutable.| Containers changes only if old image is <br/>deleted and new is used to build the container.|
 Images does not require computing resource to work.| Containers requires computing resources to run <br/> as they run as Docker Virtual Machine.|
|To make a docker image, you have to write script in Dockerfile. |To make container from image, you have to <br/>run “docker run IMAGE” command. |
|Docker Images are used to package up <br/> applications and pre-configured server environments. |Containers use server information and file system <br/> provided by image in order to operate. |
|Images can be shared on Docker Hub.|It makes no sense in sharing a running entity, <br/>always docker images are shared.|
|There is no such running state of Docker Image.|Containers uses RAM when created and in running state.|

# Docker Flow

```
DockerFile ---> (Build) ---> Image ---> (Run) ---> Container
```
**Dockerfile** : contains a set of Docker instructions that provisions your operating system the way you like, and installs/configure all your software.

**Image** : compiled Dockerfile. Saves you time from rebuilding the Dockerfile every time you need to run a container. And it's a way to hide your provision code.

**Container** : the virtual operating system itself. You can ssh into it and run any commands you wish, as if it's a real environment. You can run 1000+ containers from the same Image.

### End-to-End Workflow

```
--------------  docker build   ----------------  docker run -dt   -------------  docker exec -it   --------
| Dockerfile | --------------> |    Image     | --------------->  | Container | -----------------> | Bash |
--------------                 ----------------                   -------------                    --------
                                 ^
                                 | docker pull
                                 |
                               ----------------
                               |   Registry   |
                               ----------------
```

[<img src="https://miro.medium.com/max/600/1*joAfS_1sBhCOJzJuaAzzeg.png" width="400">]()

# Docker Commands

## Installation

**(Ubuntu Only)** To install Docker, you can go to the official website of [Docker](https://docs.docker.com/desktop/install/ubuntu/) and follow the instructions.

**Alternatively**
```
sudo apt update && install -y docker.io
```

Using Snap
```
sudo snap install docker
```


## Build an Image
To build an image, <em>**Dockerfile** </em> is required. The best practice is to create a <em>**docker** </em> folder and place the <em>**Dockerfile** </em> inside it.

```html
docker build -t <docker_image_name> <Dockerfile>
```

Example
```
docker build -t ros_bare_bones .
```


## Run an Image

```html
docker run <docker_image_name>
```
The above command will create a new image everytime we run. **Inefficient**

To run an image efficiently, we need to pass the flag `-rm` which will clean the image automatically.
```html
docker run -rm <docker_image_name>
```


## Locate List of Docker Images Locally

To find the number of docker images locally

```html
docker images ls -a
```

## Locate List of Docker Containers Locally
To find the number of docker images locally

```html
docker container ps -a
```


## Delete a Docker Container

Deleting a docker container forcefully

```html
docker rm -f <container_id>
```

If the Docker container ID is not know, use `docker container ps -a`. This will output like,
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


## Delete a Docker Image
Deleting a Docker Image forcefully

```html
docker rmi -f <docker_image_name>
```

If the Docker image ID is not know, use `docker image ls -a`. This will output like,
```
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
```

## Delete All Docker Images 

```html
sudo docker rmi -f $(docker images -aq)
```
