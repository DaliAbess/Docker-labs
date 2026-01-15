# Docker Lab #11: Start Command
## Overview
The `docker-compose start` command is used to start containers of a service. In this lab, we will explore how to use this command to start and stop containers in a Docker environment.

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
5. **Stop the container of a single service**: Run the following command to stop the `webserver` container:
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
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh  Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;  Exit 0
```
7. **Start the stopped container**: Run the following command to start the `webserver` container:
```bash
$ docker-compose start webserver
```
Expected output:
```
Starting webserver ... done
```
Note: You can't directly bring up/Start containers using `docker-compose start`.

## Key Concepts
* `docker-compose start` command is used to start containers of a service.
* `docker-compose up -d` command is used to bring up containers in detached mode.
* `docker-compose ps` command is used to check the status of containers.
* `docker-compose stop` command is used to stop a container.
* `docker-compose start` command is used to start a stopped container.

By completing this lab, you have learned how to use the `docker-compose start` command to start and stop containers in a Docker environment.

---

