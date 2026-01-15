# Docker Lab #10: Stop Command
## Overview
The `docker-compose stop` command is used to stop containers in a service. This lab will guide you through creating a `docker-compose.yml` file, bringing up containers, and stopping the container service.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. Create a `docker-compose.yml` file with the following content:
```yml
version: '3.1'
services:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: nginx
    restart: unless-stopped
    ports:
    - "80:80"
    - "443:443"
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
2. Bring up the containers using the following command:
```bash
$ docker-compose up -d
```
3. Check the container status using:
```bash
$ docker-compose ps
```
4. Stop the container service using:
```bash
$ docker-compose stop
```
5. List out the services using:
```bash
$ docker-compose ps --services
```
6. Stop a single service using:
```bash
$ docker-compose stop webserver
```

## Code Examples
The `docker-compose.yml` file contains the following services:
* `webserver`: an Nginx service with the `nginx:alpine` image
* `dbserver`: a MySQL service with the `mysql:5.7` image

## Expected Output
After running the `docker-compose ps` command, you should see the following output:
```
Name      Command               State                    Ports
------------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh  Up      0.0.0.0:3306->3306/tcp, 33060/tcp
nginx     nginx -g daemon off;   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
After running the `docker-compose stop` command, you should see the following output:
```
Stopping webserver ... done
Stopping Mysqldb      ... done
```

## Key Concepts
* `docker-compose stop`: stops containers in a service
* `docker-compose up -d`: brings up containers in detached mode
* `docker-compose ps`: checks the container status
* `docker-compose ps --services`: lists out the services
* `docker-compose stop <service_name>`: stops a single service

By completing this lab, you will learn how to use the `docker-compose stop` command to stop containers in a service, and how to manage services using `docker-compose`.

---

