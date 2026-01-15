## Lab #4: Create an Image with CMD Instruction
### Overview
This lab focuses on creating a Docker image using the `CMD` instruction. The `CMD` instruction is used to set a default command that will be executed when the container is run. In this lab, we will create a Docker image that runs the `top` command by default.

### Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

### Step-by-Step Instructions
To complete this lab, follow these steps:
1. **Create a Dockerfile**: Create a new file named `Dockerfile_cmd` with the following content:
```dockerfile
FROM alpine:3.6
RUN apk update
CMD ["top"]
```
2. **Build the Docker Container**: Run the following command to build the Docker container:
```bash
docker build -t ajeetraina/lab3_cmd . -f Dockerfile_cmd
```
3. **Run the Docker Container**: Run the following command to start the Docker container:
```bash
docker run ajeetraina/lab3_cmd:latest
```

### Expected Output
When you run the Docker container, you should see the output of the `top` command, which displays the current system processes.

### Key Concepts and Learning Objectives
This lab covers the following key concepts:
* Using the `CMD` instruction in a Dockerfile to set a default command
* Building a Docker image using the `docker build` command
* Running a Docker container using the `docker run` command
* Understanding the difference between `CMD` and other Dockerfile instructions, such as `RUN` and `ENTRYPOINT`

By completing this lab, you will gain hands-on experience with creating and running Docker containers, and understand how to use the `CMD` instruction to customize the behavior of your containers.

---

