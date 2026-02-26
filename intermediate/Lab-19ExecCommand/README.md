# Docker Compose Exec Command Lab
## Overview
In this lab, we will explore the `docker-compose exec` command, which allows us to run commands in our services. This command is similar to the `docker exec` command, but it is used specifically with `docker-compose`.

## Prerequisites
Before starting this lab, you should:
* Create an account with DockerHub
* Open the Play with Docker (PWD) Platform on your browser
* Click on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. **Setup environment**: Create a new directory for your app and navigate into it.
```bash
$ mkdir app
$ cd app
```
2. **Create a docker-compose.yml file**: Create a new file named `docker-compose.yml` with the following content:
```yml
version: '3.1'
services:
  # Webservers
  webserver:
    image: nginx:alpine
    restart: unless-stopped
    expose:
      - "80"
      - "443"
  # Load Balancer
  loadbalancer:
    image: nginx:alpine
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - webserver
    ports:
      - "80:4000"
```
3. **Create a nginx.conf file**: Create a new file named `nginx.conf` with the following content:
```nginx
user  nginx;
events {
    worker_connections  1024;
}
http {
    server {
        listen 4000;
        location / {
            proxy_pass http://webserver:80;
        }
    }
}
```
    This file will configure our load balancer.
4. **Create the compose containers**: Run the following command to create the containers:
```bash
$ docker-compose up -d --scale webserver=3
```
5. **View the containers**: Run the following command to view the containers:
```bash
$ docker-compose ps
```
6. **Execute commands in different webservers**: Run the following commands to execute commands in each webserver:
```bash
$ docker-compose exec --index=1 webserver sh -c "echo 'Welcome to webserver1' > /usr/share/nginx/html/index.html"
$ docker-compose exec --index=2 webserver sh -c "echo 'This is webserver2' > /usr/share/nginx/html/index.html"
$ docker-compose exec --index=3 webserver sh -c "echo 'Webserver3 is up' > /usr/share/nginx/html/index.html"
```
7. **Verify changes**: Run the following command to verify the changes:
```bash
$ curl http://localhost
```
    Note: You may need to run this command multiple times to verify all changes.

## Expected Output
The expected output will be the HTML content of each webserver, which should be different for each webserver.

## Key Concepts
The key concepts covered in this lab include:
* Using the `docker-compose exec` command to run commands in services
* Using the `--index` option to specify a container when there are multiple instances of a service
* Using `docker-compose` to manage multiple containers and services
* Using a load balancer to distribute traffic across multiple webservers

By completing this lab, you should have a better understanding of how to use the `docker-compose exec` command and how to manage multiple containers and services using `docker-compose`.

---

