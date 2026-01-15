# Bridge Networking Lab
## Overview
This lab is designed to help you understand how to build, manage, and use bridge networks in Docker. By the end of this lab, you will have a solid understanding of how to create and manage bridge networks, connect containers to them, and configure NAT for external access.

## Prerequisites
To complete this lab, you will need:
* A Linux-based Docker host running Docker 1.12 or higher
* The lab was built and tested using Ubuntu 16.04

## Step-by-Step Instructions
### Step 1: The Default Bridge Network
Every clean installation of Docker comes with a pre-built network called `bridge`. To verify this, run the following command:
```bash
$ docker network ls
```
This will output a list of available networks, including the `bridge` network.

The `bridge` network is associated with the `bridge` driver, and it is scoped locally, meaning it only exists on the current Docker host. All networks created with the `bridge` driver are based on a Linux bridge (a.k.a. a virtual switch).

To list the Linux bridges on your Docker host, install the `brctl` command and run:
```bash
$ apt-get install bridge-utils
$ brctl show
```
This will output a list of available bridges, including the `docker0` bridge, which is automatically created for the `bridge` network.

You can also use the `ip` command to view details of the `docker0` bridge:
```bash
$ ip a
```
### Step 2: Connect a Container to the Default Bridge Network
The `bridge` network is the default network for new containers. To create a new container and connect it to the `bridge` network, run:
```bash
$ docker run -dt ubuntu sleep infinity
```
This command will create a new container based on the `ubuntu:latest` image and run the `sleep` command to keep the container running in the background.

To verify that the container is connected to the `bridge` network, run:
```bash
$ brctl show
```
This will output the updated list of bridges, including the `docker0` bridge with the new container's interface connected.

You can also inspect the `bridge` network to see the new container attached to it:
```bash
$ docker network inspect bridge
```
### Step 3: Test Network Connectivity
To test network connectivity, ping the IP address of the container from the shell prompt of your Docker host:
```bash
$ ping 172.17.0.2
```
Replace `172.17.0.2` with the actual IP address of your container.

To log in to the container, install the `ping` program, and ping `www.dockercon.com`, run:
```bash
$ docker ps
$ docker exec -it <container_id> /bin/bash
root@<container_id>:/# apt-get update
root@<container_id>:/# apt-get install iputils-ping
root@<container_id>:/# ping www.dockercon.com
```
Replace `<container_id>` with the actual ID of your container.

### Step 4: Configure NAT for External Connectivity
To configure NAT for external connectivity, start a new NGINX container and map port 8080 on the Docker host to port 80 inside the container:
```bash
$ docker run -d -p 8080:80 nginx
```
This will start a new NGINX container and map port 8080 on the Docker host to port 80 inside the container.

## Expected Output
The expected output of the `docker network ls` command is:
```
NETWORK ID          NAME                DRIVER              SCOPE
1befe23acd58        bridge              bridge              local
726ead8f4e6b        host                host                local
ef4896538cc7        none                null                local
```
The expected output of the `brctl show` command is:
```
bridge name     bridge id       STP enabled     interfaces
docker0         8000.0242f17f89a6       no              veth3a080f
```
The expected output of the `ip a` command is:
```
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:f1:7f:89:a6 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:f1ff:fe7f:89a6/64 scope link
       valid_lft forever preferred_lft forever
```
The expected output of the `ping` command is:
```
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.069 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.052 ms
64 bytes from 172.17.0.2: icmp_seq=3 ttl=64 time=0.050 ms
64 bytes from 172.17.0.2: icmp_seq=4 ttl=64 time=0.049 ms
64 bytes from 172.17.0.2: icmp_seq=5 ttl=64 time=0.049 ms
```
## Key Concepts and Learning Objectives
* Understanding how to create and manage bridge networks in Docker
* Connecting containers to bridge networks
* Configuring NAT for external access
* Understanding the difference between the `bridge` network and the `bridge` driver
* Understanding how to use the `brctl` command to list Linux bridges
* Understanding how to use the `ip` command to view details of the `docker0` bridge
* Understanding how to use the `docker network inspect` command to inspect the `bridge` network
* Understanding how to use the `docker exec` command to log in to a container and run commands
* Understanding how to use the `ping` command to test network connectivity

---

