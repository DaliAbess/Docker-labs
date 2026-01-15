# Docker Lab #8: Images Command
## Overview
The `docker-compose images` command is used to list out images used or created by containers. In this lab, we will create a `docker-compose.yml` file with a custom image, build a container and network, bring up the containers, and list out the images used by the containers.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Setup environment**: Create a new directory for your Docker Compose project and navigate into it.
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
This Dockerfile uses the `nginx:alpine` image and adds a custom `index.html` file.

3. **Create a docker-compose.yml file**: Create a new file named `docker-compose.yml` with the following content:
```yml
version: "3.7"
services:
  webserver:
    build:
      context: .
      dockerfile: Dockerfile
    image: webapp:v1
    container_name: Nginx
    ports:
    - "80:80"
  dbserver:
    image: mysql:5.7
    container_name: Mysqldb
    restart: unless-stopped
    ports:
    - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: Pa$$w0rd
      MYSQL_USER: test
      MYSQL_PASSWORD: Pa$$w0rd123
      MYSQL_DATABASE: test
    volumes:
    - db_data:/var/lib/mysql
volumes:
  db_data:
```
This `docker-compose.yml` file defines two services: `webserver` and `dbserver`. The `webserver` service uses the custom image `webapp:v1`, while the `dbserver` service uses the `mysql:5.7` image.

4. **Bring up the containers**: Run the following command to build the images and bring up the containers:
```bash
$ docker-compose up -d
```
The `-d` option runs the containers in the background.

5. **List out the images used by the containers**: Run the following command to list out the images used by the containers:
```bash
$ docker-compose images
```
This will output a table with the following columns:
* Container
* Repository
* Tag
* Image Id
* Size

## Expected Output
The output of the `docker-compose images` command will look like this:
```
Container  Repository  Tag  Image Id      Size
-----------------------------------------------------
Mysqldb    mysql        5.7  383867b75fd2  356 MB
Nginx     webapp       v1   3454fa918c0d  20.2 MB
```
This output shows that the `mysql:5.7` image is used for the `dbserver` container, and the custom `webapp:v1` image is used for the `webserver` container.

## Key Concepts and Learning Objectives
In this lab, you learned how to:
* Create a `docker-compose.yml` file with a custom image
* Build a container and network using Docker Compose
* Bring up containers using Docker Compose
* List out the images used by containers using the `docker-compose images` command
* Understand the output of the `docker-compose images` command and how to interpret it.

---


