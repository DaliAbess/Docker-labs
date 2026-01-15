# Docker Compose Down Command Lab
## Overview
The `docker-compose down` command is used to stop and remove containers, networks, images, and volumes. This lab will guide you through the process of creating a `docker-compose.yml` file, bringing up containers, and stopping and removing them using the `down` command.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
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
2. **Bring up the containers**: Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
3. **Check container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
Expected output:
```
Name      Command               State                    Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;   Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
4. **Stop and remove containers, networks**: Run the following command to stop and remove the containers and networks:
```bash
$ docker-compose down
```
Expected output:
```
Stopping Mysqldb ... done
Stopping Nginx ... done
Removing Mysqldb ... done
Removing Nginx ... done
Removing network root_default
```
5. **Down and remove images**: Run the following command to remove images used by any service:
```bash
$ docker-compose down --rmi all
```
Note: You can also use `--rmi local` to remove only images that don't have a custom tag set by the image field.
6. **Down and remove volumes**: Run the following command to remove volumes:
```bash
$ docker-compose down --volumes
```
7. **Stop and remove containers, networks + Remove volumes, images**: Run the following command to stop and remove containers, networks, volumes, and images:
```bash
$ docker-compose down --volume --rmi all
```
Expected output:
```
Stopping Mysqldb ... done
Stopping Nginx ... done
Removing Mysqldb ... done
Removing Nginx ... done
Removing network root_default
Removing volume root_db_data
Removing image nginx:alpine
Removing image mysql:5.7
```

## Key Concepts and Learning Objectives
* Understand the `docker-compose down` command and its options
* Learn how to create a `docker-compose.yml` file and bring up containers
* Understand how to stop and remove containers, networks, volumes, and images using the `down` command
* Familiarize yourself with the `--rmi` and `--volumes` options for removing images and volumes

This lab is designed to help you understand the `docker-compose down` command and its usage in a real-world scenario. By completing this lab, you will gain hands-on experience with Docker Compose and improve your skills in managing containers, networks, and volumes.

---

