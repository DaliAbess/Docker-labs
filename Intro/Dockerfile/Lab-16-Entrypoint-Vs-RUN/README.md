# Understanding ENTRYPOINT Instruction in Dockerfile
## Overview
The `ENTRYPOINT` instruction in a Dockerfile is used to specify the executable that should be run when the container is launched. It is often used in conjunction with the `CMD` instruction, which provides default arguments to the executable. In this lab, we will explore the difference between `ENTRYPOINT` and `RUN` instructions in a Dockerfile.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To understand the difference between `ENTRYPOINT` and `RUN` instructions, follow these steps:
1. Create a new Dockerfile with the following content:
```dockerfile
# Dockerfile content
```
Note: The actual Dockerfile content is not provided in the original text. For demonstration purposes, let's assume a simple Dockerfile:
```dockerfile
FROM alpine
ENTRYPOINT ["/bin/echo"]
CMD ["Hello, World!"]
```
2. Build the Docker image using the `docker build` command:
```bash
docker build -t my-image .
```
3. Run the image without any arguments:
```bash
docker run my-image
```
4. Run the image passing a command line argument:
```bash
docker run my-image "Hello, Docker!"
```

## Expected Output
When you run the image without any arguments, you should see the default output:
```
Hello, World!
```
When you run the image with a command line argument, you should see the custom output:
```
Hello, Docker!
```
This demonstrates that `ENTRYPOINT` is meant to provide the executable, while `CMD` is used to pass default arguments to the executable.

## Key Concepts
* `ENTRYPOINT` instruction: specifies the executable to run when the container is launched
* `CMD` instruction: provides default arguments to the executable
* `RUN` instruction: used to execute commands during the build process, but not when the container is launched

By completing this lab, you should have a clear understanding of the difference between `ENTRYPOINT` and `RUN` instructions in a Dockerfile, and how to use them effectively in your Docker applications.

---

