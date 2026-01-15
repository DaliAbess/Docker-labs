# Docker Lab #14: Unpause Command
## Overview
The `docker-compose unpause` command is used to unpause paused containers of a service. In this lab, we will explore how to use this command to manage our Docker containers.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Added a new instance of Alpine OS on the right side of the screen

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
2. **Bringing up the containers**: Run the following command to bring up the containers:
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
Mysqldb   docker-entrypoint.sh ...   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
4. **Pause the services**: Run the following command to pause the services:
```bash
$ docker-compose pause
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
Name      Command               State    Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh ...   Paused   0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;   Paused   0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
6. **Unpause the service**: Run the following command to unpause the services:
```bash
$ docker-compose unpause
```
Expected output:
```
Unpausing Mysqldb
... done
Unpausing Nginx
... done
```
You can also unpause a single service by specifying the service name:
```bash
$ docker-compose unpause <service_name>
```

## Key Concepts and Learning Objectives
* Understanding the `docker-compose unpause` command and its usage
* Learning how to pause and unpause Docker containers using `docker-compose`
* Familiarity with the `docker-compose.yml` file and its configuration options
* Understanding the importance of managing container states in a Docker environment

By completing this lab, you should have a good understanding of how to use the `docker-compose unpause` command to manage your Docker containers.

---


