# Docker Compose Run Command Lab
## Overview
The `docker-compose run` command is used to run a one-time command against a service. This command starts a new container to execute the command, rather than executing it against a running container. In this lab, we will explore the usage and options of the `docker-compose run` command.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. Create a `docker-compose.yml` file with the following content:
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
2. Bring up the containers using the following command:
```bash
$ docker-compose up -d
```
3. Check the container status using the following command:
```bash
$ docker-compose ps
```
4. List out the services using the following command:
```bash
$ docker-compose ps --services
```
5. Start the webserver service container with a shell using the following command:
```bash
$ docker-compose run webserver /bin/sh
```

## Expected Output
After running the `docker-compose ps` command, you should see the following output:
```
Name          Command               State                    Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh mysqld   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;         Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
After running the `docker-compose ps --services` command, you should see the following output:
```
webserver
dbserver
```

## Key Concepts and Learning Objectives
In this lab, you learned about the `docker-compose run` command and its usage. You also learned how to:
* Create a `docker-compose.yml` file
* Bring up containers using `docker-compose up`
* Check container status using `docker-compose ps`
* List out services using `docker-compose ps --services`
* Start a service container with a shell using `docker-compose run`

Some key concepts to take away from this lab include:
* The `docker-compose run` command starts a new container to execute a command, rather than executing it against a running container
* The `docker-compose up` command brings up containers in detached mode
* The `docker-compose ps` command checks the status of containers
* The `docker-compose ps --services` command lists out services

## Docker Compose Run Command Options
The `docker-compose run` command has several options that can be used to customize its behavior. Some of these options include:
* `-d`, `--detach`: Run the container in detached mode
* `--name NAME`: Assign a name to the container
* `--entrypoint CMD`: Override the entrypoint of the image
* `-e KEY=VAL`: Set an environment variable
* `-l`, `--label KEY=VAL`: Add or override a label
* `-u`, `--user=""`: Run as a specified username or uid
* `--no-deps`: Don't start linked services
* `--rm`: Remove the container after run
* `-p`, `--publish=[]`: Publish a container's port(s) to the host
* `--service-ports`: Run the command with the service's ports enabled and mapped to the host
* `--use-aliases`: Use the service's network aliases in the network(s) the container connects to
* `-v`, `--volume=[]`: Bind mount a volume
* `-T`: Disable pseudo-tty allocation
* `-w`, `--workdir=""`: Set the working directory inside the container

---


