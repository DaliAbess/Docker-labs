# Docker Logs Command Lab
## Overview
The Docker logs command is used to view the logs of services running in Docker containers. This lab will guide you through the process of creating a `docker-compose.yml` file, bringing up containers, and checking service logs using the `docker-compose logs` command.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
### Step 1: Create a docker-compose.yml file
Create a new file named `docker-compose.yml` with the following content:
```yml
version: '3.7'
services:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: Nginx
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
  dbserver:
    image: mysql:5.7
    container_name: Mysqldb
    restart: unless-stopped
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: Pa$$w0rd
      MYSQL_USER: test
      MYSQL_PASSWORD: Pa$$w0rd123
      MYSQL_DATABASE: test
    volumes:
      - db_data:/var/lib/mysql
volumes:
  db_data:
```
### Step 2: Bringing up the containers
Run the following command to bring up the containers in detached mode:
```bash
$ docker-compose up -d
```
### Step 3: Checking container status
Run the following command to check the status of the containers:
```bash
$ docker-compose ps
```
Expected output:
```
Name         Command               State                    Ports
----------------------------------------------------------------------------------------
Mysqldb   docker-entrypoint.sh mysqld   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
Nginx     nginx -g daemon off;       Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
```
### Step 4: Checking Service logs
Run the following command to check the service logs:
```bash
$ docker-compose logs
```
This will attach to the `Mysqldb` and `Nginx` containers and display their logs.

### Step 5: Follow log output
To see live logs, access the Nginx service while checking the logs:
```bash
$ docker-compose logs -f webserver
```
This will attach to the `Nginx` container and display its logs in real-time.

### Step 6: Checking last two line logs for a service
Run the following command to check the last two lines of logs for the `webserver` service:
```bash
$ docker-compose logs --tail="2" webserver
```
This will display the last two lines of logs for the `webserver` service.

## Expected Output
The expected output will vary depending on the services and their logs. However, you should see the logs for the `Mysqldb` and `Nginx` containers, including any errors or warnings.

## Key Concepts
* The `docker-compose logs` command is used to view the logs of services running in Docker containers.
* The `--tail` option can be used to specify the number of lines to display from the end of the log.
* The `-f` option can be used to follow the log output in real-time.
* The `docker-compose ps` command is used to check the status of the containers.
* The `docker-compose up -d` command is used to bring up the containers in detached mode.

By completing this lab, you should have a good understanding of how to use the `docker-compose logs` command to view the logs of services running in Docker containers.

---

