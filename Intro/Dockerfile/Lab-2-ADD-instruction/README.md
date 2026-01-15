# Lab #2: Create an Image with ADD Instruction
## Overview
The `COPY` and `ADD` instructions in Dockerfile serve similar purposes, allowing you to copy files from a specific location into a Docker image. While `COPY` only lets you copy local files or directories from your host into the Docker image, `ADD` supports additional sources, including URLs and tar files that can be extracted directly into the destination.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To create an image with the `ADD` instruction, follow these steps:

1. **Create a Dockerfile**: Create a new file named `Dockerfile` with the following content:
```dockerfile
FROM alpine:3.5
RUN apk update
ADD http://www.vlsitechnology.org/pharosc_8.4.tar.gz .
```
2. **Build the Docker Image**: Run the following command to build the Docker image:
```bash
docker build -t saiyam911/alpine-add . -f <name of dockerfile>
```
Replace `<name of dockerfile>` with the actual name of your Dockerfile.
3. **Tag the Image**: Tag the image as `labs-add:v1.0` using the following command:
```bash
docker tag saiyam911/alpine-add saiyam911/labs-add:v1.0
```
4. **Verify the Images**: Run the following command to verify the images:
```bash
docker images
```
This should display a list of available images, including the one you just created.

## Expected Output
The output of the `docker images` command should include the `saiyam911/alpine-add` and `saiyam911/labs-add:v1.0` images:
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
saiyam911/alpine-add   latest              cdf97cb49d48        38 minutes ago      300MB
saiyam911/labs-add     v1.0                cdf97cb49d48        38 minutes ago      300MB
```
5. **Create a Container**: Create a new container based on the `labs-add:v1.0` image using the following command:
```bash
docker run -itd saiyam911/labs-add:v1.0 /bin/sh
```
6. **Verify the Container**: Run the following command to verify the container:
```bash
docker ps
```
This should display a list of running containers, including the one you just created.

## Entering the Container Shell
To enter the container shell, run the following command:
```bash
docker attach f094
```
Press the "Enter" key twice to enter the container shell.

## Verifying the Extracted Tar File
Once inside the container shell, run the following command to verify that the tar file has been extracted:
```bash
ls -ltr
```
This should display a list of files, including the extracted tar file:
```
-rw-------    1 root     root     295168000 Sep 19  2007 pharosc_8.4.tar.gz
```
The `ADD` command allows you to add a tar file directly from a URL and extract it into the container.

## Key Concepts and Learning Objectives
* Understanding the difference between `COPY` and `ADD` instructions in Dockerfile
* Using the `ADD` instruction to copy files from a URL and extract tar files into a Docker image
* Creating a Docker image and tagging it with a specific version
* Creating a container based on the Docker image and verifying its contents
* Entering the container shell and verifying the extracted tar file

By completing this lab, you should have gained hands-on experience with using the `ADD` instruction in Dockerfile and understanding its capabilities and limitations.

---


