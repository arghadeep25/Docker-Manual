[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/1280px-Docker_%28container_engine%29_logo.svg.png">]()

# Docker Compose

- Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

- It works in all environments: production, staging, development, testing, as well as CI workflows. It allows you to manage the entire lifecycle of your application, including starting, stopping, and rebuilding services, as well as viewing the status of running services and streaming the log output.

- Using Compose is basically a three-step process:
    1. Define your app’s environment with a **Dockerfile** so it can be reproduced anywhere.
    2. Define the services that make up your app in **docker-compose.yml** so they can be run together in an isolated environment.
    3. Run **docker-compose up** and Compose starts and runs your entire app.

# Docker vs Docker Compose

|                                          Docker                                           |                                        Docker Compose                                        |
| :---------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------: |
|                              Manages individual containers.                               |                           Manages multi-container applications.                              |
|                    Requires long `docker run` commands with many flags.                   |                    Uses a single `docker-compose.yml` file for config.                       |
|                      Best for simple, isolated applications.                              |                       Ideal for complex, microservice architectures.                         |
|                       Network and volumes must be created manually.                       |                  Automatically creates networks and volumes by default.                      |
|                      Harder to manage dependencies between containers.                    |              Easily defines dependencies using the `depends_on` property.                    |

# Docker Compose Architecture

```
       +-----------------------+
       |  docker-compose.yml   | <--- Configuration (Services, Networks, Volumes)
       +-----------+-----------+
                   |
                   v
       +-----------------------+
       |    Docker Compose     | <--- Orchestrator Tool
       +-----------+-----------+
                   |
     +-------------+-------------+
     |             |             |
     v             v             v
+---------+   +---------+   +---------+
| Service |   | Service |   | Service | <--- Isolated Containers
|    A    |   |    B    |   |    C    |
+---------+   +---------+   +---------+
```

# Docker Compose Flow

```
docker-compose.yml ---> (up) ---> Images (Pull/Build) ---> Networks/Volumes ---> Containers
```

**YAML File** : A configuration file (usually named `docker-compose.yml`) that defines services, networks, and volumes for a Docker application.

**Service** : A configuration for a container. For example, a web app service might use an image for a specific web server, while a database service uses an image for a database.

**Project** : A collection of services that work together to form an application. By default, the project name is the name of the directory containing the `docker-compose.yml` file.

### End-to-End Workflow

```
-------------------   docker-compose build   -------------------   docker-compose up -d   -------------------
| docker-compose.yml| ----------------------> | Prepared Images | ----------------------> | Running Services |
-------------------                           -------------------                           -------------------
         |                                                                                          |
         |                                                                                          v
         |            docker-compose down             -------------------                docker-compose logs -f
         +------------------------------------------> | Cleanup Resources | <----------------------------------
                                                      -------------------
```

# Docker Compose Commands

## Installation

Docker Compose is usually included with Docker Desktop. For Linux, you might need to install it separately.

```
sudo apt update && sudo apt install docker-compose-v2
```

## Start Services
To start all services defined in the configuration file.

```html
docker-compose up
```

To run in the background (detached mode)
```
docker-compose up -d
```

## Build or Rebuild Services
If you make changes to your Dockerfile or the source code, you may need to rebuild the images.

```html
docker-compose build
```

To build and start simultaneously
```
docker-compose up --build
```

## Stop Services
To stop the running services without removing them.

```html
docker-compose stop
```

## Down (Stop and Remove)
Stops containers and removes containers, networks, volumes, and images created by `up`.

```html
docker-compose down
```

To remove volumes as well
```
docker-compose down -v
```

## View Logs
To see the output from your services.

```html
docker-compose logs -f
```

To see logs for a specific service
```
docker-compose logs -f <service_name>
```

## List Services
To check the status of your services.

```html
docker-compose ps
```

## Execute Command in Service
To run a command within a running service container.

```html
docker-compose exec <service_name> <command>
```

Example
```
docker-compose exec web bash
```

## Check Configuration
To validate and view the Compose file.

```html
docker-compose config
```

# FAQ

### - Environment Variables not loading
If your `.env` file is not being picked up, ensure it is in the same directory as the `docker-compose.yml` file or specify it manually.

```
docker-compose --env-file <path_to_env> up
```

### - Port already allocated
If you get an error saying a port is already in use:
`Bind for 0.0.0.0:8080 failed: port is already allocated`

Check what is using the port:
```
sudo lsof -i :8080
```
Then stop the process or change the port mapping in `docker-compose.yml`.

### - How to restart a single service?
Instead of restarting everything, you can target a specific service.

```
docker-compose restart <service_name>
```

### - Using a custom filename
If your compose file is not named `docker-compose.yml`, use the `-f` flag.

```
docker-compose -f custom-compose.yml up
```

### - Orphaned Containers
If you see a warning about orphaned containers, it means there are containers running that are no longer defined in your compose file. You can remove them with:

```
docker-compose up --remove-orphans
```
