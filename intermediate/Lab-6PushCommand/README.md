# Docker Lab #6: Push Command
## Overview
The `docker-compose push` command is used to push service images to Docker Hub or a private Docker registry. In this lab, we will create a custom Docker image using a Dockerfile, build the image using `docker-compose`, and upload it to Docker Hub.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with Docker Hub
* Opened the Play with Docker (PWD) platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Create a directory structure and navigate to it**:
```bash
mkdir -p dockerlabs/{nginx,httpd} 
cd dockerlabs
```
2. **Create a Dockerfile for a custom Nginx image**:
```bash
echo 'FROM nginx:alpine
RUN echo "nginx - Welcome to Docker Workshop!" >/usr/share/nginx/html/index.html
CMD ["nginx", "-g", "daemon off;"] ' > nginx/Dockerfile_nginx
```
3. **Create a Dockerfile for a custom Httpd image**:
```bash
echo 'FROM httpd:alpine
RUN echo "httpd - Welcome to Docker Workshop!" > /usr/local/apache2/htdocs/index.html
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"] ' > httpd/Dockerfile_httpd
```
4. **Create a `docker-compose.yml` file**:
```yml
version: "3.7"
services:
  customNginx:
    build:
      context: .
      dockerfile: nginx/Dockerfile_nginx
    image: saviovettoor/custom_nginx_dockerlabs:v1
  customHttpd:
    build:
      context: .
      dockerfile: httpd/Dockerfile_httpd
    image: saviovettoor/custom_httpd_dockerlabs:v1
```
Note: Make sure the image name follows the format `<USER_NAME>/<REPOSITORY>`.

5. **Build the images using `docker-compose`**:
```bash
docker-compose build
```
6. **Check if the images have been created**:
```bash
docker image ls
```
Expected output:
```
REPOSITORY                                  TAG                 IMAGE ID            CREATED             SIZE
saviovettoor/custom_nginx_dockerlabs         v1                  3098d9cb3971        3 minutes ago       21.2MB
saviovettoor/custom_httpd_dockerlabs         v1                  866e070c373a        3 minutes ago       127MB
```
7. **Upload the images to Docker Hub**:
* Log in to Docker Hub:
```bash
docker login -u
```
* Push the images:
```bash
docker-compose push
```
Alternatively, you can push a single service image:
```bash
docker-compose push customNginx
```
Expected output:
```
Pushing customNginx (saviovettoor/custom_nginx_dockerlabs:v1)...
The push refers to repository [docker.io/saviovettoor/custom_nginx_dockerlabs]
e4f534d7f270: Pushed
3e76d2df1790: Mounted from library/nginx
03901b4a2ea8: Mounted from library/nginx
v1: digest: sha256:aa83133b840728922ad95133ff17ed95fed7d3fb89e9919925a874cf848cd282 size: 946
```

## Key Concepts and Learning Objectives
This lab covers the following key concepts:

* Creating a custom Docker image using a Dockerfile
* Building images using `docker-compose`
* Pushing images to Docker Hub using `docker-compose push`
* Understanding the format of the `docker-compose.yml` file
* Using `docker image ls` to verify image creation

By completing this lab, you will gain hands-on experience with the `docker-compose push` command and learn how to upload custom Docker images to Docker Hub.

---


