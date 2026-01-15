# Lab #8: Create an Image with ARG Instruction
## Overview
The ARG instruction in Dockerfile is used to define a parameter and its default value. This default value can be overridden by the `--build-arg` flag in the `docker build` command. In this lab, we will learn how to use the ARG instruction to create a Docker image.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:

1. **Writing a Dockerfile with ARG instruction**: Create a new Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
# Setting a default value to Argument WELCOME_USER
ARG WELCOME_USER=Collabnix
RUN echo "Welcome $WELCOME_USER, to Docker World!" > message.txt
CMD cat message.txt
```
2. **Building Docker Image with default argument**: Build the Docker image using the default argument value:
```bash
$ docker image build -t arg:v1 .
```
3. **Running container argv:v1**: Run the container using the default argument value:
```bash
$ docker run arg:v1
```
4. **Passing the argument during image build time**: Build the Docker image using a custom argument value:
```bash
$ docker image build -t arg:v2 --build-arg WELCOME_USER=Savio .
```
5. **Running container argv:v2**: Run the container using the custom argument value:
```bash
$ docker run arg:v2
```

## Code Examples
The Dockerfile used in this lab is:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
# Setting a default value to Argument WELCOME_USER
ARG WELCOME_USER=Collabnix
RUN echo "Welcome $WELCOME_USER, to Docker World!" > message.txt
CMD cat message.txt
```
The commands used to build and run the containers are:
```bash
$ docker image build -t arg:v1 .
$ docker run arg:v1
$ docker image build -t arg:v2 --build-arg WELCOME_USER=Savio .
$ docker run arg:v2
```

## Expected Output
The expected output of the containers is:
```
Welcome Collabnix, to Docker World!
```
and
```
Welcome Savio, to Docker World!
```

## Key Concepts
The key concepts learned in this lab are:
* The ARG instruction is used to define a parameter and its default value in a Dockerfile.
* The default value can be overridden by the `--build-arg` flag in the `docker build` command.
* The ARG instruction can be used to set environment variables during the build process, but these variables are not persisted in the running container.
* The ARG instruction should not be used to store sensitive information, such as passwords, as the values can be seen in the Docker history.

Note: The ARG instruction is the only instruction that can come before the FROM instruction, but the arg value can only be used by the FROM instruction.

---


