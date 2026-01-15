## Lab 17: USER Instruction under Dockerfile
### Overview
The USER directive in a Dockerfile is used to set the user identity for the commands such as RUN, CMD, and ENTRYPOINT. This instruction is similar to WORKDIR, which changes the working directory. The USER instruction affects the state of the environment and future layers, allowing you to switch to a specified user that must be pre-established.

### Prerequisites
Before proceeding with this lab, ensure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on Add New Instance on the left side of the screen to bring up an Alpine OS instance on the right side

### Step-by-Step Instructions
To work with the USER instruction in a Dockerfile, follow these steps:
1. Create a new user and group using the `groupadd` and `useradd` commands.
2. Use the USER instruction to switch to the newly created user.
3. Use the `gosu` command to change the user identity during execution, especially when running a service process with an already established user.

### Code Examples
```bash
# Create a redis user and group
RUN groupadd -r redis && useradd -r -g redis redis
# Switch to the redis user
USER redis
# Run the redis-server command
RUN [ "redis-server" ]
```
To use `gosu` to change the user identity, follow these steps:
```bash
# Create a redis user and group
RUN groupadd -r redis && useradd -r -g redis redis
# Download gosu
RUN wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64" \
&& chmod +x /usr/local/bin/gosu \
&& gosu nobody true
# Set CMD and execute it as another user
CMD [ "exec", "gosu", "redis", "redis-server" ]
```
### Expected Output
The expected output will depend on the specific commands and instructions used in your Dockerfile. Ensure that you test your Dockerfile and verify the output.

### Key Concepts and Learning Objectives
* Understanding the USER instruction in a Dockerfile
* Creating a new user and group using `groupadd` and `useradd` commands
* Switching to a newly created user using the USER instruction
* Using `gosu` to change the user identity during execution
* Best practices for running service processes with established users

Some key points to remember:
* The USER instruction affects the state of the environment and future layers.
* The specified user must be pre-established before switching to it.
* `gosu` is a recommended tool for changing user identity during execution, especially in the absence of a TTY environment.
* Avoid using `su` or `sudo` for changing user identity, as they require more cumbersome configuration.

---

 
