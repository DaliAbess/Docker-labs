# Docker Lab #5: Pull Command
## Overview
The `docker-compose pull` command is used to pull down images specified under each service in a `docker-compose` file from Docker Hub. This lab will guide you through the process of creating a `docker-compose.yml` file, pulling down service images, and pulling down the image of a single service.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. Create a `docker-compose.yml` file with the following content:
```yml
version: '3.1'
services:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: webserver
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
```
2. Pull down the service images using the following command:
```bash
$ docker-compose pull
```
This will pull down the images for both the `webserver` and `dbserver` services.

3. Check the images in your local repository using the following command:
```bash
$ docker image ls
```
This will display a list of images in your local repository, including the ones you just pulled down.

4. To pull down the image of a single service, use the following command:
```bash
$ docker-compose pull webserver
```
This will pull down only the `webserver` service image (`nginx:alpine`).

## Expected Output
After running the `docker-compose pull` command, you should see output similar to the following:
```
Pulling webserver ... done
Pulling dbserver ... done
```
After running the `docker image ls` command, you should see a list of images in your local repository, including the ones you just pulled down:
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               5.7                 383867b75fd2        2 hours ago         373MB
nginx               alpine              d87c83ec7a66        2 weeks ago         21.2MB
```
## Key Concepts and Learning Objectives
This lab covers the following key concepts and learning objectives:

* Using the `docker-compose pull` command to pull down images from Docker Hub
* Creating a `docker-compose.yml` file to specify services and images
* Pulling down images for multiple services
* Pulling down the image of a single service
* Checking images in the local repository using the `docker image ls` command

By completing this lab, you should have a good understanding of how to use the `docker-compose pull` command to manage images for your Docker services.

---


