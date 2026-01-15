# Docker Lab #18: Scale Command
## Overview
The `docker-compose scale` command is used to set the number of containers to run for a service. However, please note that the `scale` command is deprecated and it is recommended to use the `up` command with the `--scale` flag instead.

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
  redis-master:
    image: redis:latest
    container_name: webserver
    restart: unless-stopped
    ports:
    - "6379"
  redis-slave:
    image: gcr.io/google_samples/gb-redisslave:v1
    ports:
    - "6379"
    environment:
    - GET_HOSTS_FROM=dns
  frontend:
    image: gcr.io/google-samples/gb-frontend:v3
    ports:
    - "80:80"
    environment:
    - GET_HOSTS_FROM=dns
```
2. **Bringing up the containers**: Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
3. **Checking container status**: Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
This will output the following:
```
Name                  Command               State                    Ports
-------------------------------------------------------------------------------------
root_frontend_1   apache2-foreground   Up       0.0.0.0:80->80/tcp
root_redis-slave_1   /entrypoint.sh /bin/sh -c ...   Up       0.0.0.0:32769->6379/tcp
webserver           docker-entrypoint.sh redis ...   Up       0.0.0.0:32768->6379/tcp
```
4. **List out the services**: Run the following command to list out the services:
```bash
$ docker-compose ps --services
```
This will output the following:
```
redis-slave
frontend
redis-master
```
5. **Scale service**: Run the following command to scale the `redis-slave` service to 3 instances:
```bash
$ docker-compose scale redis-slave=3
```
This will output the following:
```
Starting root_redis-slave_1 ... done
Creating root_redis-slave_2 ... done
Creating root_redis-slave_3 ... done
```
6. **Checking container status again**: Run the following command to check the status of the containers again:
```bash
$ docker-compose ps
```
This will output the following:
```
Name                  Command               State                    Ports
-------------------------------------------------------------------------------------
root_frontend_1   apache2-foreground   Up       0.0.0.0:80->80/tcp
root_redis-slave_1   /entrypoint.sh /bin/sh -c ...   Up       0.0.0.0:32772->6379/tcp
root_redis-slave_2   /entrypoint.sh /bin/sh -c ...   Up       0.0.0.0:32775->6379/tcp
root_redis-slave_3   /entrypoint.sh /bin/sh -c ...   Up       0.0.0.0:32776->6379/tcp
webserver           docker-entrypoint.sh redis ...   Up       0.0.0.0:32768->6379/tcp
```

## Key Concepts and Learning Objectives
* The `docker-compose scale` command is used to set the number of containers to run for a service.
* The `scale` command is deprecated and it is recommended to use the `up` command with the `--scale` flag instead.
* The `docker-compose up` command is used to bring up the containers in detached mode.
* The `docker-compose ps` command is used to check the status of the containers.
* The `docker-compose ps --services` command is used to list out the services.

## Note
* The host machine can only bind an unallocated port to the container, so trying to scale a service which is mounted to the host will fail.
* Instead of using the `scale` command, you can use the `up` command with the `--scale` flag, for example: `docker-compose up --scale redis-slave=3`

---


