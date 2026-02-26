# Docker Lab #18: Scale Command
## Overview
The `docker-compose scale` command is used to set the number of containers to run for a service. However, please note that the `scale` command is deprecated and it is recommended to use the `up` command with the `--scale` flag instead.

## Prerequisites
Before starting this lab, make sure you have:
* Created an account with DockerHub
* Opened the Play with Docker (PWD) Platform on your browser
* Clicked on "Add New Instance" on the left side of the screen to bring up an Alpine OS instance on the right side

## Step-by-Step Instructions
# Docker Compose Scaling Demo

This project demonstrates how to use Docker Compose to scale services horizontally and load balance traffic across multiple container instances using Traefik.

## 🚀 Features

- **Auto-Discovery:** Traefik automatically detects new service instances.
- **Load Balancing:** Round-robin distribution of incoming requests.
- **Scalability:** Easily increase or decrease the number of application instances.

## 🔧 Prerequisites

- Docker installed.
- Docker Compose installed.

## 📂 Project Structure

### `docker-compose.yml`

```yaml
version: "3.8"
services:
  # The Load Balancer (Traefik)
  proxy:
    image: traefik:v2.10
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"      # Web Traffic
      - "8080:8080"  # Traefik Dashboard
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

  # The App Service to scale (whoami)
  app:
    image: traefik/whoami
    labels:
      - "traefik.http.routers.app.rule=PathPrefix(`/`)"
      - "traefik.http.services.app.loadbalancer.server.port=80"
```

## 🚦 Getting Started

### 1. Launch the Services

Start the project in detached mode:

```bash
docker-compose up -d
```

### 2. Scale the Application

Scale the `app` service to 5 instances:

```bash
docker-compose up -d --scale app=5
```

### 3. Verify Instances

Check that all 5 containers are running:

```bash
docker-compose ps
```

## 🧪 Testing the Load Balancer

### Option A: Command Line (Fastest)

Run this loop to see the different Hostnames (Container IDs) responding to your requests:

```bash
for i in {1..10}; do curl -s http://localhost | grep "Hostname"; done
```

### Option B: Browser

1. Open [http://localhost](http://localhost).
2. Refresh the page repeatedly.
3. Observe the **Hostname** and **IP** fields changing — each refresh points to a different container instance.

### Option C: Dashboard

Monitor your infrastructure at [http://localhost:8080](http://localhost:8080).

## 🧹 Cleanup

To stop the services and remove the containers:

```bash
docker-compose down
```
## Key Concepts and Learning Objectives
* The `docker-compose scale` command is used to set the number of containers to run for a service.
* The `scale` command is deprecated and it is recommended to use the `up` command with the `--scale` flag instead.
* The `docker-compose up` command is used to bring up the containers in detached mode.
* The `docker-compose ps` command is used to check the status of the containers.
* The `docker-compose ps --services` command is used to list out the services.

## Note
* The host machine can only bind an unallocated port to the container, so trying to scale a service which is mounted to the host will fail.
* Instead of using the `scale` command, you can use the `up` command with the `--scale` flag, for example: `docker-compose up --scale redis-slave=3`

---


