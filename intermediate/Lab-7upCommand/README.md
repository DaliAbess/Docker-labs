# Docker Lab #7: up Command
## Overview
The `docker-compose up` command is used to bring up a multi-container application, which is described in the `docker-compose.yml` file. This lab will guide you through creating a `docker-compose.yml` file with a custom image, building containers and networks, and bringing up the containers.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a directory for the project**: 
```bash
$ mkdir -p docker-compose/build
$ cd docker-compose/build
```
2. **Create a Dockerfile**:
```dockerfile
FROM nginx:alpine
RUN echo "Welcome to Docker Workshop!" >/usr/share/nginx/html/index.html
CMD ["nginx", "-g", "daemon off;"]
```
3. **Create a docker-compose.yml file**:
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
      MYSQL_ROOT_PASSWORD: Passw0rd
      MYSQL_USER: test
      MYSQL_PASSWORD: Passw0rd123
      MYSQL_DATABASE: test
    volumes:
    - db_data:/var/lib/mysql
volumes:
  db_data:
```
4. **Build container and network without starting the container**:
```bash
$ docker-compose up --no-start
```
    This command will create the network and containers, but will not start them.
5. **Check the status of the containers**:
```bash
$ docker-compose ps
```
    This command will show the status of the containers.
6. **Bring up the containers in detached mode**:
```bash
$ docker-compose up -d
```
    This command will build the images and bring up the containers in detached mode.
7. **Check the web server response**:
```bash
$ curl http://localhost
```
    This command should return "Welcome to Docker Workshop!".
8. **Check the db server response**:
```bash
$ docker exec -it Mysqldb mysql -u root -p
```
    This command will open a MySQL shell where you can execute queries.
9. **Rebuild the docker image and bring the stack up**:
```bash
$ docker-compose up -d --build
```
    This command will rebuild the images and bring up the containers in detached mode.

## Expected Output
After completing these steps, you should see the following output:
* "Welcome to Docker Workshop!" when you run `curl http://localhost`
* A MySQL shell when you run `docker exec -it Mysqldb mysql -u root -p`

## Key Concepts
This lab covers the following key concepts:
* Creating a `docker-compose.yml` file with a custom image
* Building containers and networks using `docker-compose up`
* Bringing up containers in detached mode using `docker-compose up -d`
* Checking the status of containers using `docker-compose ps`
* Rebuilding images and bringing up containers using `docker-compose up -d --build`

---

