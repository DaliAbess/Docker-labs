# Docker Lab #11: EXPOSE Instruction
## Overview
The EXPOSE instruction in Docker is used to expose a port, with the protocol being either UDP or TCP, associated with the indicated port. By default, the protocol is TCP if not specified. The EXPOSE instruction does not map ports on the host machine but can be overridden using the `-p` flag when starting a container.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To work with the EXPOSE instruction, follow these steps:

1. **Create an image with EXPOSE instruction**: 
    Create a Dockerfile with the following content:
```dockerfile
FROM nginx:alpine
LABEL maintainer="Collabnix"
EXPOSE 80/tcp
EXPOSE 80/udp
CMD [ "nginx","-g","daemon off;" ]
```
2. **Build the Docker image**:
    Run the following command to build the Docker image:
```bash
$ docker build -t expose:v1 .
```
3. **Create a container based on the expose:v1 image**:
    Run the following command to create a container:
```bash
$ docker container run --rm -d --name expose-inst expose:v1
```
4. **Inspect the EXPOSE port in the image**:
    Use the following command to inspect the EXPOSE port:
```bash
$ docker image inspect --format='{{range $p, $conf := .Config.ExposedPorts}}{{$p}} {{end}}' expose:v1
```
5. **Publish all exposed ports**:
    You can publish all exposed ports using the `-P` flag:
```bash
$ docker container run --rm -P -d --name expose-inst-Publish expose:v1
```
6. **Check the published port**:
    List all containers to check the published port:
```bash
$ docker container ls
```

## Expected Output
After running the `docker container ls` command, you should see the published port, similar to this:
```
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                    PORTS     NAMES
24983e09bd86   expose:v1   "nginx -g 'daemon of…"   46 seconds ago   Up 45 seconds (healthy)   0.0.0.0:32768->80/tcp, 0.0.0.0:32768->80/udp   expose-inst-Publish
```

## Key Concepts and Learning Objectives
* Understanding the EXPOSE instruction in Docker
* Creating a Docker image with EXPOSE instruction
* Inspecting exposed ports in a Docker image
* Publishing exposed ports using the `-P` flag
* Overriding EXPOSE settings using the `-p` flag

By completing this lab, you will have a better understanding of how to work with the EXPOSE instruction in Docker and how to publish exposed ports.

---

