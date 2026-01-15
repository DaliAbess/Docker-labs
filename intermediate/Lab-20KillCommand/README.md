# Lab #20: Kill Command
## Overview
This lab focuses on the `docker-compose kill` command, which is used to stop all containers started by `docker-compose`. The goal of this lab is to verify if the `kill` command successfully stops all containers and to check if there are any running containers after the command is executed.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Initial Setup**: Create a new directory and navigate into it.
   ```bash
$ mkdir app
$ cd app
```
2. **Create a docker-compose.yml file**: Create a `docker-compose.yml` file with the following content:
   ```yml
version: '3.1'
services:
  webserver:
    image: nginx:alpine
    expose:
      - "80"
  loadbalancer:
    image: nginx:alpine
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - webserver
    ports:
      - "80:4000"
```
3. **Create the compose containers**: Start the containers in detached mode and scale the `webserver` service to 3 instances.
   ```bash
$ docker-compose up -d --scale webserver=3
```
4. **View the containers**: Check the status of the containers.
   ```bash
$ docker-compose ps
```
5. **Kill all the containers**: Stop all the containers using the `kill` command.
   ```bash
$ docker-compose kill
```
6. **Check if there are any running containers**: Verify if there are any running containers after the `kill` command.
   ```bash
$ docker-compose ps
```

## Expected Output
After executing the `docker-compose kill` command, you should not see any running containers when you run `docker-compose ps`.

## Key Concepts and Learning Objectives
This lab covers the following key concepts:
* Using the `docker-compose kill` command to stop all containers
* Verifying the status of containers using `docker-compose ps`
* Understanding the difference between stopping and killing containers in Docker
* Scaling services using `docker-compose up` with the `--scale` option

By completing this lab, you will gain hands-on experience with the `docker-compose kill` command and understand its role in managing Docker containers.

---


