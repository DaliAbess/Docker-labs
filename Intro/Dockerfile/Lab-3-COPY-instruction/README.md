# Lab #3: Create an Image with COPY Instruction
## Overview
The `COPY` instruction in Docker is used to copy files or directories from a source and add them to the filesystem of a container at a specified destination. This lab will guide you through creating an image using the `COPY` instruction and demonstrate its usage in both single-stage and multi-stage builds.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Added a new instance of Alpine OS on the right side of the screen

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create an image with COPY instruction**
	* Create a new file named `index.html` with the following content:
```bash
$ echo "Welcome to Dockerlabs !" > index.html
```
	* Create a `Dockerfile` with the following content:
```dockerfile
FROM nginx:alpine
LABEL maintainer="Collabnix"
COPY index.html /usr/share/nginx/html/
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```
	* Build the Docker image:
```bash
$ docker image build -t cpy:v1 .
```
	* Start a new container from the image:
```bash
$ docker container run -d --rm --name myapp1 -p 80:80 cpy:v1
```
	* Check the index file:
```bash
$ curl localhost
```
2. **COPY instruction in Multi-stage Builds**
	* Create a new `Dockerfile` with the following content:
```dockerfile
FROM alpine AS stage1
LABEL maintainer="Collabnix"
RUN echo "Welcome to Docker Labs!" > /opt/index.html
FROM nginx:alpine
LABEL maintainer="Collabnix"
COPY --from=stage1 /opt/index.html /usr/share/nginx/html/
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```
	* Build the Docker image:
```bash
$ docker image build -t cpy:v2 .
```
	* Start a new container from the image:
```bash
$ docker container run -d --rm --name myapp2 -p 8080:80 cpy:v2
```
	* Check the index file:
```bash
$ curl localhost:8080
```

## Expected Output
After completing the above steps, you should see the following output:
* For the single-stage build:
```bash
Welcome to Dockerlabs !
```
* For the multi-stage build:
```bash
Welcome to Docker Labs !
```

## Key Concepts and Learning Objectives
This lab covers the following key concepts and learning objectives:
* Understanding the `COPY` instruction in Docker
* Creating an image using the `COPY` instruction
* Using the `COPY` instruction in multi-stage builds
* Understanding the `--from` flag in the `COPY` instruction
* Creating and running containers from the built images

Some important notes to keep in mind:
* You can name your stages by adding an `AS` keyword to the `FROM` instruction.
* By default, stages are not named, and you can refer to them by their integer number, starting with 0 for the first `FROM` instruction.
* You can use the `COPY --from` instruction to copy from a separate image, either using the local image name, a tag available locally, or on a Docker registry.
* Example:
```bash
COPY --from=nginx:latest /etc/nginx/nginx.conf /nginx.conf
```

---

