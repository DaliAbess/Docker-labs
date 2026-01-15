# Docker Lab #1: Create an Image with GIT Installed
## Overview
This lab guides you through creating a Docker image with GIT installed, tagging the image, and verifying the installation by running a container based on the image. The goal is to understand the process of creating a custom Docker image and using it to deploy a container with specific software installed.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a Dockerfile**: Define a Dockerfile that installs GIT on an Alpine Linux base image.
2. **Build the Docker Image**: Use the Dockerfile to build a custom Docker image.
3. **Tag the Image**: Tag the image with a specific name and version.
4. **Verify the Images**: List all available Docker images to confirm the creation of the new image.
5. **Create a Container**: Run a container based on the newly created image.
6. **Enter the Container Shell**: Attach to the running container and enter its shell.
7. **Verify GIT Installation**: Check if GIT is installed correctly by running the `git --version` command.

### Creating the Dockerfile
```dockerfile
FROM alpine:3.5
RUN apk update
RUN apk add git
```
This Dockerfile uses the Alpine Linux 3.5 image as a base, updates the package list, and installs GIT.

### Building the Docker Image
```bash
docker build -t ajeetraina/alpine-git .
```
This command builds the Docker image using the instructions in the Dockerfile and tags it as `ajeetraina/alpine-git`.

### Tagging the Image
```bash
docker tag ajeetraina/alpine-git ajeetraina/labs-git:v1.0
```
This command tags the `ajeetraina/alpine-git` image as `ajeetraina/labs-git:v1.0`.

### Verifying the Images
```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ajeetraina/alpine-git   latest              cb913e37a593        16 seconds ago      26.6MB
ajeetraina/labs-git     v1.0                cb913e37a593        16 seconds ago      26.6MB
```
This command lists all available Docker images, showing the newly created images.

### Creating a Container
```bash
docker run -itd ajeetraina/labs-git:v1.0 /bin/sh
```
This command runs a container based on the `ajeetraina/labs-git:v1.0` image and starts a shell session.

### Entering the Container Shell
```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND     CREATED         STATUS                    PORTS     NAMES
3e26a5268f55   ajeetraina/labs-git:v1.0   "/bin/sh"   4 seconds ago   Up 2 seconds (healthy)   0.0.0.0:0->0.0.0.0:0   elated_neumann

docker attach 3e26
```
Press the "Enter" key twice to enter the container shell.

### Verifying GIT Installation
```bash
/ # git --version
git version 2.13.7
```
This command checks if GIT is installed correctly by displaying its version.

## Key Concepts and Learning Objectives
This lab covers the following key concepts:
* Creating a custom Docker image using a Dockerfile
* Installing software packages in a Docker image
* Tagging and versioning Docker images
* Running containers based on custom images
* Verifying software installation in a container

By completing this lab, you will gain hands-on experience with creating and using custom Docker images, which is essential for deploying and managing containerized applications.

---


