# Docker Compose Build Command Lab
## Overview
In this lab, we will explore the Docker Compose build command, which is used to create a new image using the instructions in the Dockerfile. The build can be specified either as a string containing a path to the build context. The newly built image will be used to create the container for the service.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on Add New Instance on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. **Setup environment**: Create a new directory for the lab and navigate into it.
```bash
$ mkdir -p docker-compose/build
$ cd docker-compose/build
```
2. **Create a Dockerfile**: Create a new file named `Dockerfile` with the following content:
```dockerfile
FROM nginx:alpine
RUN echo "Welcome to Docker Workshop!" >/usr/share/nginx/html/index.html
CMD ["nginx", "-g", "daemon off;"]
```
This Dockerfile uses the `nginx:alpine` image, adds a custom index.html file, and sets the command to run the nginx server.

3. **Create a docker-compose.yml file**: Create a new file named `docker-compose.yml` with the following content:
```yml
version: "3.7"
services:
  webapp:
    build:
      context: .
      dockerfile: Dockerfile
    image: webapp:v1
```
This docker-compose file specifies the build context, Dockerfile, and image name for the `webapp` service.

4. **Build the image using docker-compose**: Run the following command to build the image:
```bash
$ docker-compose build
```
This command will build the image with the name `webapp` and tag `v1`.

5. **Check the image**: Run the following command to verify that the image has been created:
```bash
$ docker image ls webapp:v1
```

## Key Concepts and Learning Objectives
* The `docker-compose build` command is used to create a new image using the instructions in the Dockerfile.
* The `build` directive in the docker-compose file specifies the path to the folder where the Dockerfile is located.
* The `context` directive specifies the build context directory that is sent to the Docker daemon.
* The `dockerfile` directive specifies the Dockerfile filename.
* The `image` directive specifies the name and tag of the image.
* The `--force-rm` option removes the temporary container during the build process.
* The `--no-cache` option does not use cache during the build image process.
* The `--pull` option always tries to get a mirror of the updated version.

## Additional Options and Directives
* `args`: specifies the variables when the image is built.
* `cache_from`: specifies the cache to build the image.
Example:
```yml
version: '3'
services:
  webapp:
    build:
      context: ./dir
      dockerfile: Dockerfile-alternate
      args:
        buildno: 1
      cache_from:
        - alpine:latest
        - corp/web_app:3.14
```
Note: This lab is designed to provide a comprehensive understanding of the Docker Compose build command and its various options and directives. By completing this lab, you will gain hands-on experience with building images using Docker Compose.

---
