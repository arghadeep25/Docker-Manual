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


|                                          Docker Image                                           |                                        Docker Container                                        |
| :---------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------: |
|                                   Blueprint of the Container.                                   |                                     Instance of the Image.                                     |
|                                   Image is a logical entity.                                    |                               Container is a real world entity.                                |
|                                      Images are immutable.                                      |  Containers changes only if old image is <br/>deleted and new is used to build the container.  |
|                       Images does not require computing resource to work.                       |  Containers requires computing resources to run <br/> as they run as Docker Virtual Machine.   |
|                 To make a docker image, you have to write script in Dockerfile.                 |         To make container from image, you have to <br/>run “docker run IMAGE” command.         |
| Docker Images are used to package up <br/> applications and pre-configured server environments. | Containers use server information and file system <br/> provided by image in order to operate. |
|                               Images can be shared on Docker Hub.                               |      It makes no sense in sharing a running entity, <br/>always docker images are shared.      |
|                         There is no such running state of Docker Image.                         |                     Containers uses RAM when created and in running state.                     |

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

#### Platform Specific

In case having issue to build an image on different platform for example AMD64 or ARM/v7, include the flag to avoid the error
```
docker build --platform <platform_name> -t <image_name> <DOCKER_FILE_PATH>
```

Example

```
docker build --platform linux/amd64 -t ros_bare_bones .
```

## Run an Image

```html
docker run <docker_image_name>
```
The above command will create a new image everytime we run. **Inefficient**

To run an image efficiently, we need to pass the flag `-rm` which will clean the image automatically.
```html
docker run --rm -it --name=<docker_image_name> <docker_image_name>
```

## Pause and Unpause a Docker Container

```html
docker pause <docker_container_name>
```

```html
docker unpause <docker_container_name>
```

## Stop a Docker Container

```
docker stop <docker_container_name>
```

## Restart a Docker Container

```
docker restart <docker_container_name>
```


## Get Inside Docker Container
To enter a Docker container, first run the image with a specified name and run the following command

```html
docker exec -it <docker_container_name> bash
```

## Get Docker Logs

```html
docker logs <docker_container_name> --tail=<numer_of_logs> -ft
```

```html
docker logs test_container --tail=50 -ft
```

## Inspect a Docker Container [Low-Level Infos (JSON Format)]

```html
docker inspect <docker_container_name>
```

## List of Processes Running in a Docker Container

```html
docker top <docker_container_name>
```

## Copy from Docker Container to Local

```
sudo docker cp <docker_container_name>:/file/path/within/container /host/path/target
```
Example
```
sudo docker cp goofy_roentgen:/out_read.jpg .
```

## Locate
### - Locate List of Docker Images Locally

To find the number of docker images locally

```html
docker images ls -a
```

### - Locate List of Docker Containers Locally
To find the number of docker images locally

```html
docker container ps -a
```
or (Only IDs)
```
docker ps -aq
```

## Delete

### - Delete a Docker Container

Deleting a docker container forcefully

```html
docker rm -f <container_id>
```

If the Docker container ID is not known, use `docker container ps -a`. This will output like,
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


### - Delete all Docker Containers

To delete all Docker Containers at once

```
docker rm $(docker ps -aq)
```

### - Delete a Docker Image
Deleting a Docker Image forcefully

```html
docker rmi -f <docker_image_name>
```

If the Docker image ID is not known, use `docker image ls -a`. This will output like,
```
REPOSITORY     TAG       IMAGE ID       CREATED          SIZE
```

### - Delete All Docker Images 

```html
docker rmi -f $(docker images -aq)
```


## Stop All Running Docker Containers

To stop all running Docker containers

```
docker stop $(docker ps -aq)
```

## Change Docker Directory

In case you are facing the issue of root directory is full, it's better to move the default docker directory(`/var/lib/docker`) from root to somewhere else. To do that, we need to follow few steps

#### - Stop Docker
```
sudo systemctl stop docker.service docker.socket
```

#### Create New Directory for Docker
```
mkdir /home/arghadeep/docker
```

#### - Create New Docker Configuration
```
sudo touch /etc/docker/daemon.json
sudo vim /etc/docker/daemon.json
```

#### - Insert New Path
```
{
  "data-root": "/new/path/docker-data"
}

Example:

{
  "data-root": "/home/arghadeep/docker"
}

```

#### - Add Permission
```
sudo chown -R root:docker /new/path/docker-data

Example:
sudo chown -R root:docker /home/arghadeep/docker/
```

#### - Move Existing Data to New Directory
```
sudo rsync -aP /var/lib/docker/ /new/path/docker-data/

Example:
sudo rsync -aP /var/lib/docker/ /home/arghadeep/docker/
```


# FAQ

### - Permission Denied Issue
If you get this error 

`docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.35/containers/create: dial unix /var/run/docker.sock: connect: permission denied. See 'docker run --help'.`

Run the following command

```
sudo chmod 666 /var/run/docker.sock
```

Or you can go through [Permission Issue Stackoverflow](https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue)



### - Unable to delete <image_tag> (cannot be forced) - image has dependent child images

If you are getting this error, try using this command

```
docker rmi $(docker images --filter "dangling=true" -q --no-trunc)
```


### - WARNING: Error loading config file
Changing the ownership and permissions using the following commands can fix the permission issue with the configuration file.

```
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "/home/$USER/.docker" -R
```


### - Cannot connect to the Docker daemon
Start the Docker services

```
sudo systemctl start docker.service
sudo systemctl start docker.socket
```


### - Error response from daemon: conflict

Check the containers 
```
docker ps -a
```
This will return the output like
```
CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES
```
Now delete the container forcefully

```html
docker rm -f <container_name>
```