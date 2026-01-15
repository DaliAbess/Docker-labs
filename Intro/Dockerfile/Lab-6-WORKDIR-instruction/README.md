# Lab #6: WORKDIR Instruction
## Overview
The WORKDIR instruction in a Dockerfile defines the working directory for the rest of the instructions in the Dockerfile. This instruction does not create a new layer in the image but adds metadata to the image config. If the WORKDIR does not exist, it will be created even if it's not used in any subsequent Dockerfile instruction. You can have multiple WORKDIR instructions in the same Dockerfile. If a relative path is provided, it will be relative to the previous WORKDIR instruction.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. Create a Dockerfile with a WORKDIR instruction
2. Build a Docker image using the Dockerfile
3. Test the current WORKDIR by running a container
4. Repeat steps 1-3 for different WORKDIR scenarios (relative path, absolute path, environment variables as path)

### Dockerfile with WORKDIR Instruction
Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
WORKDIR /opt
```
Build the Docker image using the following command:
```bash
$ docker build -t workdir:v1 .
```
Test the current WORKDIR by running a container:
```bash
$ docker run -it workdir:v1 pwd
```
Expected output: `/opt`

### WORKDIR with Relative Path
Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
WORKDIR /opt
RUN echo "Welcome to Docker Labs" > opt.txt
WORKDIR folder1
RUN echo "Welcome to Docker Labs" > folder1.txt
WORKDIR folder2
RUN echo "Welcome to Docker Labs" > folder2.txt
```
Build the Docker image using the following command:
```bash
$ docker build -t workdir:v2 .
```
Test the current WORKDIR by running a container:
```bash
$ docker run -it workdir:v2 pwd
```
Expected output: `/opt/folder1/folder2`

### WORKDIR with Absolute Path
Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
WORKDIR /opt/folder1
RUN echo "Welcome to Docker Labs" > opt.txt
WORKDIR /var/tmp/
```
Build the Docker image using the following command:
```bash
$ docker build -t workdir:v3 .
```
Test the current WORKDIR by running a container:
```bash
$ docker run -it workdir:v3 pwd
```
Expected output: `/var/tmp`

### WORKDIR with Environment Variables as Path
Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
ENV DIRPATH /myfolder
WORKDIR $DIRPATH
```
Build the Docker image using the following command:
```bash
$ docker build -t workdir:v4 .
```
Test the current WORKDIR by running a container:
```bash
$ docker run -it workdir:v4 pwd
```
Expected output: `/myfolder`

## Key Concepts
* The WORKDIR instruction defines the working directory for the rest of the instructions in the Dockerfile.
* The WORKDIR instruction does not create a new layer in the image but adds metadata to the image config.
* If the WORKDIR does not exist, it will be created even if it's not used in any subsequent Dockerfile instruction.
* You can have multiple WORKDIR instructions in the same Dockerfile.
* If a relative path is provided, it will be relative to the previous WORKDIR instruction.
* The WORKDIR instruction can resolve environment variables previously set in the Dockerfile using the ENV instruction.

---

