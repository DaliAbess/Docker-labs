# Docker Networking Basics
## Overview
This lab covers the basic networking components that come with a fresh installation of Docker. You will learn how to use the `docker network` command to configure and manage container networks.

## Description
In this lab, you will complete the following steps:
* Learn about the `docker network` command
* List existing networks
* Inspect a network
* List network driver plugins

## Prerequisites
To complete this lab, you will need:
* A Linux-based Docker Host running Docker 1.12 or higher

## Step-by-Step Instructions
### Step 1: The docker network command
The `docker network` command is the main command for configuring and managing container networks. Run the following command to view the usage and available sub-commands:
```bash
$ docker network
```
Expected output:
```
Usage:
  docker network COMMAND

Manage Docker networks

Options:
      --help   Print usage

Commands:
  connect     Connect a container to a network
  create       Create a network
  disconnect   Disconnect a container from a network
  inspect      Display detailed information on one or more networks
  ls           List networks
  rm           Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.
```
### Step 2: List networks
Run the following command to view existing container networks on the current Docker host:
```bash
$ docker network ls
```
Expected output:
```
NETWORK ID          NAME                DRIVER              SCOPE
1befe23acd58        bridge              bridge              local
726ead8f4e6b        host                host                local
ef4896538cc7        none                null                local
```
### Step 3: Inspect a network
Use the `docker network inspect` command to view network configuration details. The following command shows the details of the network called `bridge`:
```bash
$ docker network inspect bridge
```
Expected output:
```json
[
    {
        "Name": "bridge",
        "Id": "1befe23acd58cbda7290c45f6d1f5c37a3b43de645d48de6c1ffebd985c8af4b",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Containers": {},
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```
### Step 4: List network driver plugins
Run the following command to view the list of network plugins:
```bash
$ docker info
```
Expected output:
```
Containers: 0
Running: 0
Paused: 0
Stopped: 0
Images: 0
Server Version: 1.12.3
Storage Driver: aufs
...
Plugins:
 Volume: local
 Network: bridge host null overlay
Swarm: inactive
Runtimes: runc
...
```
## Key Concepts
* The `docker network` command is used to configure and manage container networks.
* The `docker network ls` command is used to list existing networks.
* The `docker network inspect` command is used to view network configuration details.
* The `docker info` command is used to view the list of network plugins.
* The available network drivers are `bridge`, `host`, `null`, and `overlay`.

---

