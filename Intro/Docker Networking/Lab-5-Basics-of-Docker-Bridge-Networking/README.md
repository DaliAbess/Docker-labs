# Bridge Networking with Docker
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
This will output the list of available networks, including the `bridge` network.

The output will look something like this:
```
NETWORK ID          NAME                DRIVER              SCOPE
1befe23acd58        bridge              bridge              local
726ead8f4e6b        host                host                local
ef4896538cc7        none                null                local
```
As you can see, the `bridge` network is associated with the `bridge` driver and is scoped locally, meaning it only exists on this Docker host.

To inspect the Linux bridges on your Docker host, install the `brctl` command and run:
```bash
# Install the brctl tools
$ apt-get install bridge-utils

# List the bridges on your Docker host
$ brctl show
```
This will output the list of available bridges, including the `docker0` bridge:
```
bridge name     bridge id       STP enabled     interfaces
docker0         8000.0242f17f89a6       no
```
You can also use the `ip` command to view details of the `docker0` bridge:
```bash
$ ip a
```
This will output the IP address and other details of the `docker0` bridge:
```
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:f1:7f:89:a6 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:f1ff:fe7f:89a6/64 scope link
       valid_lft forever preferred_lft forever
```
### Step 2: Connect a Container to the Default Bridge Network
The `bridge` network is the default network for new containers. To create a new container and connect it to the `bridge` network, run:
```bash
$ docker run -dt ubuntu sleep infinity
```
This will create a new container based on the `ubuntu:latest` image and run the `sleep` command to keep the container running in the background.

To verify that the container is connected to the `bridge` network, run:
```bash
$ brctl show
```
This will output the updated list of bridges, including the `docker0` bridge with the new container connected:
```
bridge name     bridge id       STP enabled     interfaces
docker0         8000.0242f17f89a6       no              veth3a080f
```
You can also inspect the `bridge` network to see the new container attached to it:
```bash
$ docker network inspect bridge
```
This will output the details of the `bridge` network, including the connected containers:
```
"Containers": {
    "6dd93d6cdc806df6c7812b6202f6096e43d9a013e56e5e638ee4bfb4ae8779ce": {
        "Name": "reverent_dubinsky",
        "EndpointID": "dda76da5577960b30492fdf1526c7dd7924725e5d654bed57b44e1a6e85e956c",
        "MacAddress": "02:42:ac:11:00:02",
        "IPv4Address": "172.17.0.2/16",
        "IPv6Address": ""
    }
},
```
### Step 3: Test Network Connectivity
To test the network connectivity, ping the IP address of the container from the shell prompt of your Docker host:
```bash
$ ping 172.17.0.2
```
This will output the ping results:
```
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.069 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.052 ms
64 bytes from 172.17.0.2: icmp_seq=3 ttl=64 time=0.050 ms
64 bytes from 172.17.0.2: icmp_seq=4 ttl=64 time=0.049 ms
64 bytes from 172.17.0.2: icmp_seq=5 ttl=64 time=0.049 ms
^C
--- 172.17.0.2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 3999ms
rtt min/avg/max/mdev = 0.049/0.053/0.069/0.012 ms
```
To test the network connectivity from within the container, log in to the container and install the `ping` program:
```bash
# Get the ID of the container started in the previous step.
$ docker ps

# Exec into the container
$ docker exec -it 6dd93d6cdc80 /bin/bash

# Update APT package lists and install the iputils-ping package
root@6dd93d6cdc80:/# apt-get update
root@6dd93d6cdc80:/# apt-get install iputils-ping

# Ping www.dockercon.com from within the container
root@6dd93d6cdc80:/# ping www.dockercon.com
```
This will output the ping results:
```
PING www.dockercon.com (104.239.220.248) 56(84) bytes of data.
64 bytes from 104.239.220.248: icmp_seq=1 ttl=39 time=93.9 ms
64 bytes from 104.239.220.248: icmp_seq=2 ttl=39 time=93.8 ms
64 bytes from 104.239.220.248: icmp_seq=3 ttl=39 time=93.8 ms
^C
--- www.dockercon.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 93.878/93.895/93.928/0.251 ms
```
### Step 4: Configure NAT for External Connectivity
To configure NAT for external connectivity, start a new NGINX container and map port 8080 on the Docker host to port 80 inside the container:
```bash
$ docker run -d -p 8080:80 nginx
```
This will create a new container based on the `nginx:latest` image and map port 8080 on the Docker host to port 80 inside the container.

## Key Concepts and Learning Objectives
* Bridge networks in Docker
* Creating and managing bridge networks
* Connecting containers to bridge networks
* Configuring NAT for external connectivity
* Testing network connectivity

By completing this lab, you should have a solid understanding of how to build, manage, and use bridge networks in Docker, as well as how to configure NAT for external connectivity.

---

