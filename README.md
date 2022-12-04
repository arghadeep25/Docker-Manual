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

- A Docker image executes code in a Docker container. You add a writable layer of core functionalities on a Docker image to create a running container.

# Docker Commands


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


## List of Docker Images Locally

To find the number of docker images locally

```html
docker images ls -a
```


## Delete a Docker Image

```
docker rm 
```


## Delete All Docker Images 

```html
sudo docker rmi -f $(docker images -aq)
```
