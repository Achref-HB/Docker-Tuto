# Docker-Tuto

## Setup Docker

- To install the latest version of Docker, run:
  `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

- Verify that the installation is successful by running the hello-world image:
  `sudo docker run hello-world`

## Docker Basics

Docker is a containerization solution that offer a way to package software and make it run on any OS/Hardware.

- *Dockerfile* is a blueprint for building a Docker image.

- *Docker image* is a template for a Docker container.

- *Docker container* is a running process that package software.

- *Dockerignore* file is required when you don't want to add some files to the image.

- *Docker volume* is a folder on the host machine that can persised data and share it between host and a container or even between multiple containers.

- *Docker compose* is a tool for running multiple docker containers at the same time.

## Docker commands

### General commands

- Start the docker daemon
    `docker -d`
- Get help with Docker. Can also use –help on all subcommands
    `docker --help`
- Display system-wide information
    `docker info`

### Images

- Build an Image from a Dockerfile
    `docker build -t <image_name> .`
- Build an Image from a Dockerfile without the cache
    `docker build -t <image_name> . –no-cache`
- List local images
    `docker images`
- Delete an Image
    `docker rmi <image_name>`
- Remove all unused images
    `docker image prune`

### Docker Hub

- Login into Docker
    `docker login -u <username>`
- Publish an image to Docker Hub
    `docker push <username>/<image_name>`
- Search Hub for an image
    `docker search <image_name>`
- Pull an image from a Docker Hub
    `docker pull <image_name>`

### Containers

- Create and run a container from an image, with a custom name:
    `docker run --name <container_name> <image_name>`
- Run a container with and publish a container’s port(s) to the host.
    `docker run -p <host_port>:<container_port> <image_name>`
- Run a container in the background
    `docker run -d <image_name>`
- Start or stop an existing container:
    `docker start|stop <container_name> (or <container-id>)`
- Remove a stopped container:
    `docker rm <container_name>`
- Open a shell inside a running container:
    `docker exec -it <container_name> sh`
- Fetch and follow the logs of a container:
    `docker logs -f <container_name>`
- To inspect a running container:
    `docker inspect <container_name> (or <container_id>)`
- To list currently running containers:
    `docker ps`
- List all docker containers (running and stopped):
    `docker ps --all`
- View resource usage stats
    `docker container stats`

## Docker Basics Tutorial with Node.js

1. Develop a simple express server to run as the container’s process.
2. Create a Dockerfile that contains node runtime, packages, server ports and dependecies.
3. Create a Dockerignore file is required so we don’t add the node_modules folder to the image.
4. Build the Docker Image.
   `docker build -t node/demoapp:1.0 .`
5. Run the Container
   `docker run -d -p 5000:8080 <image-id>`
6. Create a docker volume to persised data
   `docker volume create <volume-name>`
7. Run a Container with the Volume
   `docker run -d -p 5000:8080 -v my_volume:/app/data node/demoapp:1.0`
8. Access the running container
   `sudo docker exec -it <container_id> sh`
9. Navigate to the mounted directory (/app/data) and create a test file
    `cd /app/data`
    `echo "Hello from Docker volume!" > test.txt`
    `exit`

10. Check the Data on the Host
    `cd /var/lib/docker/volumes/my_volume/_data`
    `ls`
    `cat test.txt`
11. Run Docker Compose to make it easier to manage multiple containers and volumes.
    `docker-compose up`
