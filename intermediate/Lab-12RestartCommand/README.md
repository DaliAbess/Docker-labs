# Docker Lab #12: Restart Command
## Overview
The `docker-compose restart` command is used to restart services in a Docker environment. This lab will guide you through the process of creating a `docker-compose.yml` file, creating containers and networks, and restarting services using the `docker-compose restart` command.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a `docker-compose.yml` file**: Create a new file named `docker-compose.yml` with the following content:
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
2. **Create the container and network**: Run the following command to create the container and network:
```bash
$ docker-compose up --no-start
```
This will create a new network and container, but will not start them.

3. **Check container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
This will display the status of the containers.

4. **List out the services**: Run the following command to list out the services:
```bash
$ docker-compose ps --services
```
This will display the names of the services.

5. **Restart the service**: Run the following command to restart the services:
```bash
$ docker-compose restart
```
This will restart all the services.

6. **Check container status again**: Run the following command to check the status of the containers again:
```bash
$ docker-compose ps
```
This will display the updated status of the containers.

7. **Restart a single service**: Run the following command to restart a single service:
```bash
$ docker-compose restart webserver
```
This will restart the `webserver` service.

8. **Set a time wait for stop before killing the container**: Run the following command to set a time wait for stop before killing the container:
```bash
$ docker-compose restart -t 30 webserver
```
This will set a timeout of 30 seconds before killing the container.

## Expected Output
After running the above commands, you should see the following output:
```
Creating network "root_default" with the default driver
Creating Mysqldb ... done
Creating Nginx ... done
```
And when you check the container status:
```
Name   Command               State                    Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh mysqld   Up       0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx    nginx -g daemon off;       Up       0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
## Key Concepts
This lab covers the following key concepts:
* Creating a `docker-compose.yml` file
* Creating containers and networks using `docker-compose up`
* Restarting services using `docker-compose restart`
* Checking container status using `docker-compose ps`
* Listing out services using `docker-compose ps --services`
* Restarting a single service using `docker-compose restart <service_name>`
* Setting a time wait for stop before killing the container using `docker-compose restart -t <timeout> <service_name>`

---

