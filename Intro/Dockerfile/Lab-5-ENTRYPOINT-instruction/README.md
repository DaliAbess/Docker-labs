# Docker Lab #5: Create an Image with ENTRYPOINT Instruction
## Overview
The ENTRYPOINT instruction in Docker allows you to make your container run as an executable. This lab will guide you through creating an image with the ENTRYPOINT instruction in both Exec Form and Shell Form, as well as overriding the existing ENTRYPOINT.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
### Create an Image with ENTRYPOINT Instruction (Exec Form)
1. Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.5
LABEL maintainer="Collabnix"
ENTRYPOINT ["/bin/echo", "Hi, your ENTRYPOINT instruction in Exec Form !"]
```
2. Build the Docker image using the following command:
```bash
$ docker build -t entrypoint:v1 .
```
3. Verify the image using the following command:
```bash
$ docker image ls
```
Expected output:
```
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
entrypoint   v1        1d06f06c2062   2 minutes ago   4MB
alpine       3.5       f80194ae2e0c   7 months ago    4MB
```
4. Create a container using the following command:
```bash
$ docker container run entrypoint:v1
```
Expected output:
```
Hi, your ENTRYPOINT instruction in Exec Form !
```

### ENTRYPOINT Instruction in Shell Form
1. Create a Dockerfile with the following content:
```dockerfile
FROM alpine:3.5
LABEL maintainer="Collabnix"
ENTRYPOINT echo "Hi, your ENTRYPOINT instruction in Shell Form !"
```
2. Build the Docker image using the following command:
```bash
$ docker build -t entrypoint:v2 .
```
3. Verify the image using the following command:
```bash
$ docker image ls
```
Expected output:
```
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
entrypoint   v2        cde521f13080   2 minutes ago   4MB
entrypoint   v1        1d06f06c2062   5 minutes ago   4MB
alpine       3.5       f80194ae2e0c   7 months ago    4MB
```
4. Create a container using the following command:
```bash
$ docker container run entrypoint:v2
```
Expected output:
```
Hi, your ENTRYPOINT instruction in Shell Form !
```

### Override the Existing ENTRYPOINT
1. Use the following command to override the existing ENTRYPOINT:
```bash
$ docker container run --entrypoint "/bin/echo" entrypoint:v2 "Hello, Welcome to Docker Meetup! "
```
Expected output:
```
Hello, Welcome to Docker Meetup!
```

## Key Concepts and Learning Objectives
* The ENTRYPOINT instruction can be used in both Exec Form and Shell Form.
* The ENTRYPOINT instruction makes your container run as an executable.
* To override the existing ENTRYPOINT, use the `--entrypoint` flag when running the container.
* The `--entrypoint` flag allows you to specify a new ENTRYPOINT for the container.

## Contributor
This lab was contributed by Savio Mathew.

---

