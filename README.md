[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/1280px-Docker_%28container_engine%29_logo.svg.png">]()


## Build an Image
To build an image, <em>**Dockerfile** </em> is required. The best practice is to create a <em>**docker** </em> folder and place the <em>**Dockerfile** </em> inside it.


```
docker build -t <docker_image_name> <Dockerfile>
```

Example
```
docker build -t ros_bare_bones .
```

## Run an Image

```
docker run <docker_image_name>
```
The above command will create a new image everytime we run. **Inefficient**

To run an image efficiently, we need to pass the flag `-rm` which will clean the image automatically.
```
docker run -rm <docker_image_name>
```

## List of Docker Images

To find the number of docker images locally

```
docker images ls -a
```

## Delete a Docker Image

```
docker rm 
```

## Delete All Docker Images 

```
sudo docker rmi -f $(docker images -aq)
```
