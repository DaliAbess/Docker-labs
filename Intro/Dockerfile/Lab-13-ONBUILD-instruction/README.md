# ONBUILD Instruction in Docker
## Overview
The ONBUILD instruction in Docker is a special instruction that allows you to create a base image that can be used by other images. When an image is built using the ONBUILD instruction, the instructions specified after ONBUILD are not executed immediately. Instead, they are stored and executed when another image is built using the current image as a base.

## Description
The ONBUILD instruction is useful when you want to create a base image that can be used by multiple projects. By using ONBUILD, you can create a base image that contains common instructions that can be shared across multiple projects. When a new project is built using the base image, the instructions specified after ONBUILD are executed, allowing the project to customize the base image.

## Prerequisites
* Docker installed on your system
* Basic understanding of Docker and Dockerfile

## Step-by-Step Instructions
To use the ONBUILD instruction, follow these steps:

1. Create a base image with the ONBUILD instruction:
```dockerfile
FROM node:slim
RUN mkdir /app
WORKDIR /app
CMD [ "npm", "start" ]
```
2. Build the base image:
```bash
docker build -t my-node .
```
3. Create a new project that uses the base image:
```dockerfile
FROM my-node
```
4. Build the new project:
```bash
docker build -t my-project .
```
5. The instructions specified after ONBUILD in the base image are executed during the build process of the new project.

## Code Examples
Here are some examples of using the ONBUILD instruction:

### Node.js Example
```dockerfile
FROM node:slim
RUN mkdir /app
WORKDIR /app
CMD [ "npm", "start" ]
```
```dockerfile
FROM my-node
COPY ./package.json /app
RUN [ "npm", "install" ]
COPY . /app/
```
### Ubuntu Rails Example
```dockerfile
FROM ubuntu:12.04
RUN apt-get update -qq && apt-get install -y ca-certificates sudo curl git-core
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8
RUN curl -L https://get.rvm.io | bash -s stable
ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN /bin/bash -l -c rvm requirements
RUN source /usr/local/rvm/scripts/rvm && rvm install ruby
RUN rvm all do gem install bundler
ONBUILD ADD . /opt/rails_demo
ONBUILD WORKDIR /opt/rails_demo
ONBUILD RUN rvm all do bundle install
ONBUILD CMD rvm all do bundle exec rails server
```
```dockerfile
FROM sangam14/docker_onbuild
```
## Expected Output
When you build the new project, you should see the instructions specified after ONBUILD being executed. For example:
```bash
Step 0 : FROM cpuguy83/no_echo_here
Executing 1 build triggers
Step onbuild-0 : RUN echo "You won't see me until later"
---&gt; Running in ebfede7e39c8
You won't see me until later
---&gt; ca6f025712d4
---&gt; ca6f025712d4
Successfully built ca6f025712d4
```
## Key Concepts
* ONBUILD instruction: a special instruction that allows you to create a base image that can be used by other images.
* Base image: an image that contains common instructions that can be shared across multiple projects.
* Child image: an image that uses a base image as a starting point and can customize the base image using the ONBUILD instruction.

By following these steps and examples, you should be able to create a base image using the ONBUILD instruction and use it to build new projects. This allows you to share common instructions across multiple projects and customize the base image for each project.

---

