# Lab #14: Create a Docker Image with HEALTHCHECK Instruction
## Overview
The HEALTHCHECK directive in Docker tells the Docker engine how to determine if the state of a container is normal. This instruction was introduced in Docker 1.12 and allows for more robust health checking of containers. Before the introduction of HEALTHCHECK, Docker could only determine if a container was in an abnormal state by checking if the main process had exited. However, this approach had limitations, as a container could be in a deadlock or infinite loop state without exiting, yet still be unable to provide services.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
### Writing a Dockerfile with HEALTHCHECK Instruction
To add a health check to a simple web service, you can use the following Dockerfile:
```dockerfile
FROM nginx:1.13
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
EXPOSE 80
```
This Dockerfile sets a health check to run every 30 seconds, with a timeout of 3 seconds. If the health check command does not respond within 3 seconds, it is considered a failure.

### Building the Docker Image
To build the Docker image, run the following command:
```bash
docker image build -t nginx:1.13 .
```

### Checking the Nginx Config File Exists
To check if the Nginx config file exists, run the following command:
```bash
docker run --name=nginx-proxy -d \
  --health-cmd='stat /etc/nginx/nginx.conf || exit 1' \
  nginx:1.13
```

### Checking if Nginx is Healthy
To check if the Nginx container is healthy, run the following command:
```bash
docker inspect --format='{{.State.Health.Status}}' nginx-proxy
```

### Making the Docker Container Unhealthy and Checking
To make the Docker container unhealthy, run the following command:
```bash
docker exec nginx-proxy rm /etc/nginx/nginx.conf
```
Then, check the health status of the container again:
```bash
sleep 5; docker inspect --format='{{.State.Health.Status}}' nginx-proxy
```

### Creating the Nginx.conf File and Making the Container Healthy
To create the Nginx config file and make the container healthy again, run the following command:
```bash
docker exec nginx-proxy touch /etc/nginx/nginx.conf
```
Then, check the health status of the container again:
```bash
sleep 5; docker inspect --format='{{.State.Health.Status}}' nginx-proxy
```

## Expected Output
After running the above commands, you should see the following output:
* The Docker container should be in a healthy state initially
* After removing the Nginx config file, the container should become unhealthy
* After recreating the Nginx config file, the container should become healthy again

## Key Concepts and Learning Objectives
* Understanding the HEALTHCHECK instruction in Docker
* Learning how to write a Dockerfile with a HEALTHCHECK instruction
* Understanding how to build and run a Docker image with a HEALTHCHECK instruction
* Learning how to check the health status of a Docker container
* Understanding how to make a Docker container unhealthy and healthy again

Note: The HEALTHCHECK instruction can only appear once in a Dockerfile. If multiple HEALTHCHECK instructions are written, only the last one will take effect. The options supported by the HEALTHCHECK instruction include:
* `--interval=<interval>`: The interval between two health checks (default is 30 seconds)
* `--timeout=<time length>`: The timeout period for the health check command (default is 30 seconds)
* `--retries=<number>`: The number of consecutive failures before the container is considered unhealthy (default is 3)

---

