# Lab #9: ENV Instruction
## Overview
The ENV instruction in Dockerfile is used to set environment variables for a container when it starts. This lab will guide you through creating a Dockerfile with the ENV instruction, building a Docker image, and running a container with the specified environment variable.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. **Write a Dockerfile with ENV instruction**: Create a new file named `Dockerfile` with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
ENV WELCOME_MESSAGE="Welcome to Docker World"
CMD ["sh", "-c", "echo $WELCOME_MESSAGE"]
```
2. **Build a Docker Image**: Run the following command to build a Docker image with the tag `env:v1`:
```bash
$ docker build -t env:v1 .
```
3. **Run a container with the `env:v1` image**: Run the following command to start a new container from the `env:v1` image:
```bash
$ docker container run env:v1
```
4. **Override existing env while running a container**: Run the following command to start a new container from the `env:v1` image and override the `WELCOME_MESSAGE` environment variable:
```bash
$ docker container run --env WELCOME_MESSAGE="Welcome to Docker Workshop" env:v1
```

## Expected Output
After running the container with the `env:v1` image, you should see the following output:
```
Welcome to Docker World
```
After overriding the `WELCOME_MESSAGE` environment variable, you should see the following output:
```
Welcome to Docker Workshop
```

## Key Concepts and Learning Objectives
This lab covers the following key concepts and learning objectives:
* Understanding the ENV instruction in Dockerfile
* Setting environment variables for a container
* Overriding environment variables when running a container
* Building a Docker image with a custom Dockerfile
* Running a container from a Docker image

## Contributor
This lab was contributed by Savio Mathew.

---


