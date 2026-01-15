# Docker Lab #13: Pause Command
## Overview
The `docker-compose pause` command is used to pause services. In this lab, we will learn how to create a `docker-compose.yml` file, bring up containers, and pause services using the `docker-compose pause` command.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
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
2. **Bringing up the containers**: Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
3. **Checking container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
Expected output:
```
Name      Command               State                 Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
4. **Pause the services**: Run the following command to pause the services:
```bash
$ docker-compose pause
```
You can also pause a single service by running:
```bash
$ docker-compose pause <service_name>
```
Expected output:
```
Pausing Nginx
... done
Pausing Mysqldb
... done
```
5. **Checking container status after pause**: Run the following command to check the status of the containers after pausing:
```bash
$ docker-compose ps
```
Expected output:
```
Name      Command               State      Ports
-----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh   Paused     0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;   Paused     0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```

## Key Concepts and Learning Objectives
* Understanding the `docker-compose pause` command and its usage
* Creating a `docker-compose.yml` file and bringing up containers
* Pausing services using the `docker-compose pause` command
* Checking container status using the `docker-compose ps` command

By completing this lab, you will gain hands-on experience with the `docker-compose pause` command and learn how to pause services in a Docker environment.

---


