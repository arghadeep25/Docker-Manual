[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/1280px-Docker_%28container_engine%29_logo.svg.png">]()

# Docker Image


# Docker Container 


# Docker Image vs Docker Container 


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
