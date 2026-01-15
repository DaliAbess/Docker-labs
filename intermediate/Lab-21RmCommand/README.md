# Docker Lab #21: Rm Command
## Overview
The `docker-compose rm` command is used to remove stopped containers. In this lab, we will explore how to use this command to remove containers of stopped services.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on Add New Instance on the left side of the screen to bring up an Alpine OS instance on the right side

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
2. **Bring up the containers**: Run the following command to bring up the containers:
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
Mysqldb   docker-entrypoint.sh  Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;  Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
4. **List out the services**: Run the following command to list out the services:
```bash
$ docker-compose ps --services
```
Expected output:
```
webserver
dbserver
```
5. **Stop the container of a single service**: Run the following command to stop the container of the `webserver` service:
```bash
$ docker-compose stop webserver
```
Expected output:
```
Stopping Nginx ... done
```
6. **Check container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
Expected output:
```
Name      Command               State                    Ports
----------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh  Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;  Exit 0
```
7. **Remove the container of a stopped service**: Run the following command to remove the container of the stopped `webserver` service:
```bash
$ docker-compose rm
```
Expected output:
```
Going to remove Nginx
Are you sure? [yN] y
Removing Nginx ... done
```
Note: You can use the `-f` or `--force` flag to skip asking for confirmation to remove the container.
8. **Check container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
Expected output:
```
Name      Command               State                    Ports
---------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh  Up      0.0.0.0:3306->3306/tcp, 33060/tcp
```
9. **Stop and remove the container of a service**: Run the following command to stop and remove the container of the `dbserver` service:
```bash
$ docker-compose rm -fs dbserver
```
Expected output:
```
Stopping Mysqldb ... done
Going to remove Mysqldb
Removing Mysqldb ... done
```
Note: By default, anonymous volumes attached to containers are not removed. You can override this with the `-v` flag.

## Key Concepts
In this lab, we learned how to use the `docker-compose rm` command to remove stopped containers. We also learned how to:

* Create a `docker-compose.yml` file to define services
* Bring up containers using `docker-compose up -d`
* Check container status using `docker-compose ps`
* Stop containers using `docker-compose stop`
* Remove containers using `docker-compose rm`
* Use flags like `-f` and `-v` to customize the behavior of the `docker-compose rm` command.

---


