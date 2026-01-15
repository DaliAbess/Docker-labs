# Docker Lab #3: Config Command
## Overview
The `docker-compose config` command is used to validate the `docker-compose.yml` file and view the compose file. This lab will guide you through creating a `docker-compose.yml` file, validating it, and testing the `docker-compose config` command with a wrong configuration.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
To complete this lab, follow these steps:
1. Create a `docker-compose.yml` file
2. Validate the `docker-compose.yml` file using the `docker-compose config` command
3. Test the `docker-compose config` command with a wrong configuration

### Step 1: Create a `docker-compose.yml` file
Create a new file named `docker-compose.yml` and copy the following contents:
```yml
version: '3.1'
services:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: webserver
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
```
Alternatively, you can clone the repository:
```bash
git clone https://github.com/collabnix/dockerlabs
cd intermediate/workshop/compose/lab/3/config/
cat docker-compose.yml
```

### Step 2: Validate the `docker-compose.yml` file
Run the following command to validate the `docker-compose.yml` file:
```bash
docker-compose config
```
The expected output is:
```yml
services:
  webserver:
    container_name: webserver
    image: nginx:alpine
    ports:
    - 80:80/tcp
    - 443:443/tcp
    restart: unless-stopped
version: '3.1'
```

### Step 3: Test the `docker-compose config` command with a wrong configuration
Let's change the instruction `services` to `service` and test:
```yml
version: '3.1'
service:
  # Nginx Service
  webserver:
    image: nginx:alpine
    container_name: webserver
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
```
Run the following command:
```bash
docker-compose config
```
The expected output is an error message:
```
ERROR: The Compose file './docker-compose.yml' is invalid because:
Invalid top-level property "service". Valid top-level sections for this Compose file are: services, secrets, version, networks, volumes, and extensions starting with "x-".
You might be seeing this error because you're using the wrong Compose file version. Either specify a supported version (e.g "2.2" or "3.3") and place your service definitions under the `services` key, or omit the `version` key and place your service definitions at the root of the file to use version 1.
For more on the Compose file format versions, see https://docs.docker.com/compose/compose-file/
```

## Key Concepts and Learning Objectives
* Understanding the `docker-compose config` command and its purpose
* Creating a valid `docker-compose.yml` file
* Validating a `docker-compose.yml` file using the `docker-compose config` command
* Identifying and troubleshooting errors in the `docker-compose.yml` file
* Understanding the different sections and properties in a `docker-compose.yml` file, such as `services`, `version`, and `ports`

---


