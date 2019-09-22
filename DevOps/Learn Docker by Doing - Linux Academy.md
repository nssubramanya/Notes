# Learn Docker by Doing - Linux Academy

## Running first Docker container

### Install docker from the default CentOS 7 repository
After logging into the server, install the latest version of Docker using yum.

```
$ sudo yum -y install docker
```
### Enable & start docker service
Once installation completes, enable & start the service using systemd.

```
$ systemctl enable docker
$ systemctl start docker
```
### User permissions
Create a new group named docker, then add the cloud_user user to the group.

```
$ sudo groupadd docker
$ sudo usermod -aG docker cloud_user
```

Note: After creating group and adding user to the new docker group, login-and-logout for changes to take effect. If not, reboot the system and login again.

Check by looking at groups-

```
$ groups
cloud_user wheel docker
```
### Check if docker is working

```
$ docker help

Usage:	docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/Users/subramanyans/.docker")
  -D, --debug              Enable debug mode

```
### Get information of Docker Server & client

```
$ docker info
Containers: 3
 Running: 3
 Paused: 0
 Stopped: 0

```

### Run a docker image from repository: hello-world
After starting & enabling Docker, run the hello-world container image to verify installation.

```
$ docker run docker.io/hello-world
```

Here, `docker.io` is repository name or User name and `hello-world` is image name. The `latest` version is downloaded

### Pull images
After getting a valid return message from the hello-world image, pull the following images into your Docker repository to prepare for the next exercise.

06kellyjac/nyancat
jeremy646/doge

```
$ docker pull 06kellyjac/nyancat
$ docker pull jeremy646/doge
```

### Show the images downloaded

```
$ docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
docker.io/hello-world          latest              fce289e99eb9        5 months ago        1.84 kB
docker.io/jeremy646/doge       latest              cddd2b20f7ed        7 months ago        111 MB
docker.io/06kellyjac/nyancat   latest              329bb91b174b        11 months ago       782 kB
```

## Hosting a Static Website on Docker

### Hosting Website using nginx

* Create Directory to hold the website

```
$ mkdir website
$ cd website
$ touch index.html
$ touch Dockerfile
```
* Create `index.html` and `Dockerfile`

__index.html__

```
<!DOCTYPE html>
<html>
	<head>
		<title>Hello</title>
	</head>
	<body>
		<h1>Hello World!</h1>
	<body>
</html>
```

__Dockerfile__

```
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

* Build the Docker image

```
$ docker build -t mywebsite:v1 .
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM nginx:alpine
 ---> bfba26ca350c
Step 2/2 : COPY index.html /usr/share/nginx/html/index.html
 ---> a6df9dea5daf
Successfully built a6df9dea5daf
Successfully tagged mywebsite:v1

```
The built image will have name mywebsite with a tag of v1

* Verify whether image is created using `docker images`

```
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mywebsite           v1                  a6df9dea5daf        33 seconds ago      20.5MB
```
* Run Docker image
Expose port 80 on container to 80 on host

```
$ docker run -d -p 80:80 mywebsite:v1
ca7ec0ff77cdcb6cad03b664499c60acb6f5f680b0edd225b2863096827436a9
```

* Check if Website is running

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
ca7ec0ff77cd        mywebsite:v1        "nginx -g 'daemon of…"   25 seconds ago      Up 24 seconds       0.0.0.0:80->80/tcp   infallible_mcnulty
```
* Check if Website is giving output

```
$ curl localhost
<!DOCTYPE html>
<html>
	<head>
		<title>Hello</title>
	</head>
	<body>
		<h1>Hello World!</h1>
	<body>
</html>
```

## Building Container Images

## Create Docker file
* STEP 1: Select Base Image

```
FROM <image-name>:<tag>
FROM <image>[@<digest>] [AS <name>]

FROM nginx:1.11-alpine

ARG CODE_VERSION=latest
FROM busybox:${CODE_VERSION}
```
* Prefer to use version number and not `latest` since it may not be predictable
* FROM can appear multiple times in a single Dockerfile

* STEP 2: Other Commands
There can be other commands like-
 - COPY: Copy files from current directory to folders in image
 - RUN: Run Specific shell commands
 - CMD
 - LABEL
 - Comments
 - MAINTAINER: Name of Maintainer
 - EXPOSE: Expose Ports
 - ENV: Set Environment variables
 - ADD: Copies new files/dirs/remote URLs and adds them to FS of image
 - ENTRYPOINT: Configure container that will run as executable
 - VOLUME: Attach externally mounted volumes
 - USER: Sets user-name, user-group to use when running image
 - WORKDIR: Set Working Directory
 - ARG: Defines Variables
 - ONBUILD: Trigger when image is used as base of another build
 - STOPSIGNAL: EXIT
 - HEALTHCHECK: Test if Container is working
 - SHELL: Override shell commands

### Example Dockerfile

```
FROM nginx:1.11-alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
### Docker Build

```
$ docker build -t my-nginx-website:latest .
```
### Launch Image

```
$ docker run -d -p 80:80 my-nginx-website:latest
```

## Dockerizing Node.js application
### Base Directory
Assume that an Express application is already present

```
$ express helloApp
$ cd helloApp
$ npm install
$ npm start
```
Access application on `http://localhost:3000'

Create `.dockerignore` file in base directory `helloApp`

__.dockerignore__

```
**/node_modules
```

__Dockerfile__

Create Dockerfile in `helloApp` folder.

```
FROM node:10-alpine
RUN mkdir -p /src/app
WORKDIR /src/app
COPY package.json /src/app/package.json
RUN npm install
COPY . /src/app
EXPOSE 3000
CMD ["npm", "start"]
```

