# Docker Lab #16: Port Command
## Overview
The `docker-compose port` command is used to print the public/network facing port for a service. In this lab, we will explore how to use this command to check the external port binded to a service.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a docker-compose.yml file**: Create a new file named `docker-compose.yml` with the following content:
```yml
version: '3.7'
services:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: Nginx
    restart: unless-stopped
    ports:
      - "8080:80"
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
2. **Bringing up the containers**: Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
3. **Checking container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
4. **List out the services**: Run the following command to list out the services:
```bash
$ docker-compose ps --services
```
5. **Check the external port binded to service webserver for port 80**: Run the following command to check the external port binded to the `webserver` service for port 80:
```bash
$ docker-compose port webserver 80
```

## Expected Output
The expected output of the above commands is:
* The `docker-compose ps` command will show the status of the containers, including the ports they are using.
* The `docker-compose ps --services` command will list out the services, including `webserver` and `dbserver`.
* The `docker-compose port webserver 80` command will output the external port binded to the `webserver` service for port 80, which in this case is `0.0.0.0:8080`.

## Key Concepts
The key concepts covered in this lab are:
* Using the `docker-compose port` command to check the external port binded to a service
* Creating a `docker-compose.yml` file to define services and their ports
* Bringing up containers in detached mode using the `docker-compose up -d` command
* Checking the status of containers using the `docker-compose ps` command
* Listing out services using the `docker-compose ps --services` command

By completing this lab, you will have a better understanding of how to use the `docker-compose port` command and how to work with services and ports in Docker Compose.

---

