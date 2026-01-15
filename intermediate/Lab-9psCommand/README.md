# Docker Lab #9: ps Command
## Overview
The `docker-compose ps` command is used to list out the containers with details like status, port mapping, etc., which is declared in the `docker-compose` file. This lab will guide you through creating a `docker-compose.yml` file, bringing up containers, checking container status, and listing out services.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a docker-compose.yml file**: Create a new file named `docker-compose.yml` with the following content:
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
2. **Bring up the containers**: Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
3. **Checking container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
4. **List out Services**: Run the following command to list out the services:
```bash
$ docker-compose ps --services
```

## Expected Output
After running the `docker-compose ps` command, you should see an output similar to this:
```
Name               Command               State                    Ports
------------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh mysqld   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
nginx     nginx -g daemon off;         Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
And after running the `docker-compose ps --services` command, you should see an output similar to this:
```
webserver
dbserver
```

## Key Concepts and Learning Objectives
This lab covers the following key concepts and learning objectives:
* Creating a `docker-compose.yml` file
* Bringing up containers using `docker-compose up`
* Checking container status using `docker-compose ps`
* Listing out services using `docker-compose ps --services`
* Understanding the `docker-compose ps` command and its options

By completing this lab, you should have a good understanding of how to use the `docker-compose ps` command to manage and monitor your containers.

---


