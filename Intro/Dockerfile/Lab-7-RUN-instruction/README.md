## Lab #7: RUN Instruction
### Overview
The RUN instruction is used to execute commands on top of the current layer and create a new layer in a Dockerfile. This lab will cover the basics of the RUN instruction, including its two forms: shell form and exec form.

### Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

### Step-by-Step Instructions
To create an image with the RUN instruction, follow these steps:
1. Create a new Dockerfile with the following content:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
RUN apk add --update
RUN apk add curl
RUN rm -rf /var/cache/apk/
```
2. Build the Docker image using the following command:
```bash
$ docker image build -t run:v1 .
```
3. Check the layers of the image using the following command:
```bash
$ docker image history run:v1
```
4. Check the size of the image using the following command:
```bash
$ docker image ls run:v1
```

### Combining Multiple RUN Instructions
To combine multiple RUN instructions into one, you can use the following syntax:
```dockerfile
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
RUN apk add --update && \
    apk add curl && \
    rm -rf /var/cache/apk/
```
Then, build the Docker image using the following command:
```bash
$ docker image build -t run:v2 .
```
5. Check the layers of the image using the following command:
```bash
$ docker image history run:v2
```
6. Check the size of the image using the following command:
```bash
$ docker image ls run:v2
```

### Expected Output
The expected output for the first image (run:v1) is:
* 6 layers
* Image size: 8.42MB

The expected output for the second image (run:v2) is:
* 4 layers
* Image size: 7.08MB

### Key Concepts
The key concepts covered in this lab are:
* The RUN instruction and its two forms: shell form and exec form
* Creating a new layer in a Dockerfile using the RUN instruction
* Combining multiple RUN instructions into one
* Building and checking the layers and size of a Docker image

### Code Examples
The code examples used in this lab are:
```dockerfile
# Example 1: Multiple RUN instructions
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
RUN apk add --update
RUN apk add curl
RUN rm -rf /var/cache/apk/

# Example 2: Combined RUN instructions
FROM alpine:3.9.3
LABEL maintainer="Collabnix"
RUN apk add --update && \
    apk add curl && \
    rm -rf /var/cache/apk/
```
The commands used in this lab are:
* `docker image build -t run:v1 .`
* `docker image history run:v1`
* `docker image ls run:v1`
* `docker image build -t run:v2 .`
* `docker image history run:v2`
* `docker image ls run:v2`

---

