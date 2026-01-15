# Bridge Networking Lab
## Overview
In this lab, you will learn how to build, manage, and use bridge networks in Docker. You will complete the following steps:
* Step 1: The default bridge network
* Step 2: Connect a container to the default bridge network
* Step 3: Test the network connectivity
* Step 4: Configure NAT for external access

## Description
Bridge networking is a fundamental concept in Docker, allowing containers to communicate with each other and the host machine. In this lab, you will learn how to work with the default bridge network, connect containers to it, test network connectivity, and configure NAT for external access.

## Prerequisites
To complete this lab, you will need:
* A Linux-based Docker host running Docker 1.12 or higher
* The lab was built and tested using Ubuntu 16.04

## Step-by-Step Instructions
### Step 1: The default bridge network
Every clean installation of Docker comes with a pre-built network called `bridge`. Verify this with the `docker network ls` command.
```bash
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
1befe23acd58        bridge              bridge              local
726ead8f4e6b        host                host                local
ef4896538cc7        none                null                local
```
The output above shows that the `bridge` network is associated with the `bridge` driver. It’s essential to note that the network and the driver are connected, but they are not the same.

Install the `brctl` command and use it to list the Linux bridges on your Docker host.
```bash
# Install the brctl tools
$ apt-get install bridge-utils

# List the bridges on your Docker host
$ brctl show
bridge name     bridge id       STP enabled     interfaces
docker0         8000.0242f17f89a6       no
```
The output above shows a single Linux bridge called `docker0`. This is the bridge that was automatically created for the `bridge` network. You can see that it has no interfaces currently connected to it.

You can also use the `ip` command to view details of the `docker0` bridge.
```bash
$ ip a
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:f1:7f:89:a6 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:f1ff:fe7f:89a6/64 scope link
       valid_lft forever preferred_lft forever
```

### Step 2: Connect a container
The `bridge` network is the default network for new containers. This means that unless you specify a different network, all new containers will be connected to the `bridge` network.

Create a new container.
```bash
$ docker run -dt ubuntu sleep infinity
6dd93d6cdc806df6c7812b6202f6096e43d9a013e56e5e638ee4bfb4ae8779ce
```
This command will create a new container based on the `ubuntu:latest` image and will run the `sleep` command to keep the container running in the background. As no network was specified on the `docker run` command, the container will be added to the `bridge` network.

Run the `brctl show` command again.
```bash
$ brctl show
bridge name     bridge id       STP enabled     interfaces
docker0         8000.0242f17f89a6       no              veth3a080f
```
Notice how the `docker0` bridge now has an interface connected. This interface connects the `docker0` bridge to the new container just created.

Inspect the `bridge` network again to see the new container attached to it.
```bash
$ docker network inspect bridge
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

### Step 3: Test network connectivity
The output to the previous `docker network inspect` command shows the IP address of the new container. In the previous example, it is “172.17.0.2” but yours might be different.

Ping the IP address of the container from the shell prompt of your Docker host. Remember to use the IP of the container in your environment.
```bash
$ ping 172.17.0.2
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
Press Ctrl-C to stop the ping. The replies above show that the Docker host can ping the container over the `bridge` network.

Log in to the container, install the `ping` program, and ping `www.dockercon.com`.
```bash
# Get the ID of the container started in the previous step.
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              NAMES
6dd93d6cdc80        ubuntu              "sleep infinity"     5 minutes ago       Up 5 minutes          reverent_dubinsky

# Exec into the container
$ docker exec -it 6dd93d6cdc80 /bin/bash

# Update APT package lists and install the iputils-ping package
root@6dd93d6cdc80:/# apt-get update
root@6dd93d6cdc80:/# apt-get install iputils-ping

# Ping www.dockercon.com from within the container
root@6dd93d6cdc80:/# ping www.dockercon.com
PING www.dockercon.com (104.239.220.248) 56(84) bytes of data.
64 bytes from 104.239.220.248: icmp_seq=1 ttl=39 time=93.9 ms
64 bytes from 104.239.220.248: icmp_seq=2 ttl=39 time=93.8 ms
64 bytes from 104.239.220.248: icmp_seq=3 ttl=39 time=93.8 ms
^C
--- www.dockercon.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 93.878/93.895/93.928/0.251 ms
```
This shows that the new container can ping the internet and therefore has a valid and working network configuration.

### Step 4: Configure NAT for external connectivity
In this step, you will start a new NGINX container and map port 8080 on the Docker host to port 80 inside of the container. This means that traffic that hits the Docker host on port 8080 will be passed on to port 80 inside the container.

## Key Concepts and Learning Objectives
* Bridge networking in Docker
* Creating and managing bridge networks
* Connecting containers to bridge networks
* Testing network connectivity
* Configuring NAT for external access

By completing this lab, you will have gained hands-on experience with bridge networking in Docker and will be able to:
* Create and manage bridge networks
* Connect containers to bridge networks
* Test network connectivity
* Configure NAT for external access

---

