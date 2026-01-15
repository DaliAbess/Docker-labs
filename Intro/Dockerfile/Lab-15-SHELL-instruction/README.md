# Creating an Image with SHELL Instruction
## Overview
This lab guide provides a step-by-step tutorial on creating a Docker image using the SHELL instruction. The SHELL instruction allows you to override the default shell used for the shell form of commands in a Dockerfile. This is particularly useful on Windows, where there are multiple native shells available, including cmd and powershell.

## Prerequisites
Before starting this lab, ensure you have:
* Created an account with DockerHub
* Opened the PWD Platform on your browser
* Added a new instance of Alpine OS
* Installed the latest version of Docker

## Step-by-Step Instructions
To create an image with the SHELL instruction, follow these steps:
1. **Install Docker**: Ensure you have the latest version of Docker installed on your system.
2. **Understand SHELL instruction syntax**: The SHELL instruction syntax is `SHELL ["executable", "parameters"]`. This instruction must be written in JSON form in a Dockerfile.
3. **Create a Dockerfile**: Create a new file named `Dockerfile` with the following instructions:
```dockerfile
FROM windowsservercore
# Executed as cmd /S /C echo default
RUN echo default
# Executed as cmd /S /C powershell -command Write-Host default
RUN powershell -command Write-Host default
# Executed as powershell -command Write-Host hello
SHELL ["powershell", "-command"]
RUN Write-Host hello
# Executed as cmd /S /C echo hello
SHELL ["cmd", "/S", "/C"]
RUN echo hello
```
4. **Build the Docker image**: Run the following command to build the Docker image:
```bash
docker build -t shell .
```
5. **Verify the output**: The output should show the steps involved in building the image, including the execution of the SHELL instructions.

## Code Examples
The following code examples demonstrate the use of the SHELL instruction:
* Using the SHELL instruction to override the default shell:
```dockerfile
SHELL ["powershell", "-command"]
RUN New-Item -ItemType Directory C:\Example
ADD Execute-MyCmdlet.ps1 c:\example\
RUN c:\example\Execute-MyCmdlet -sample 'hello world'
```
* Using the JSON form of the RUN command:
```dockerfile
RUN ["powershell", "-command", "Execute-MyCmdlet", "-param1 \"c:\\foo.txt\""]
```
* Using the escape parser directive:
```dockerfile
# escape=`
FROM windowsservercore
SHELL ["powershell","-command"]
RUN New-Item -ItemType Directory C:\Example
ADD Execute-MyCmdlet.ps1 c:\example\
RUN c:\example\Execute-MyCmdlet -sample 'hello world'
```

## Expected Output
The expected output of the `docker build` command is:
```
PS E:\docker\build\shell> docker build -t shell .
Sending build context to Docker daemon 3.584 kB
Step 1 : FROM windowsservercore
---> 5bc36a335344
Step 2 : SHELL powershell -command
---> Running in 87d7a64c9751
---> 4327358436c1
Removing intermediate container 87d7a64c9751
Step 3 : RUN New-Item -ItemType Directory C:\Example
---> Running in 3e6ba16b8df9
Directory: C:\
Mode
LastWriteTime
Length Name
----
-------------
------
d-----
6/2/2016
2:59 PM
Example
---> 1f1dfdcec085
Removing intermediate container 3e6ba16b8df9
Step 4 : ADD Execute-MyCmdlet.ps1 c:\example\
---> 6770b4c17f29
Removing intermediate container b139e34291dc
Step 5 : RUN c:\example\Execute-MyCmdlet -sample 'hello world'
---> Running in abdcf50dfd1f
Hello from Execute-MyCmdlet.ps1 - passed hello world
---> ba0e25255fda
Removing intermediate container abdcf50dfd1f
Successfully built ba0e25255fda
```

## Key Concepts and Learning Objectives
The key concepts and learning objectives of this lab include:
* Understanding the SHELL instruction and its syntax
* Using the SHELL instruction to override the default shell in a Dockerfile
* Creating a Docker image using the SHELL instruction
* Understanding the difference between the shell form and JSON form of commands in a Dockerfile
* Using the escape parser directive to modify the behavior of the SHELL instruction
* Applying the SHELL instruction to modify the way a shell operates, such as delayed environment variable expansion semantics on Windows.

---

