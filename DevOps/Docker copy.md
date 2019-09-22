# Docker

### Get Docker Installation Path
```
~ $ ls -l `which docker`
lrwxr-xr-x  1 subramanyans  staff  54 Jan 16 09:47 /usr/local/bin/docker -> /Applications/Docker.app/Contents/Resources/bin/docker
```

### Get Docker Version
```
$ docker --version
Docker version 18.09.1, build 4c52b90
```

### Get Docker Version - Details
```
$ docker version
Client: Docker Engine - Community
 Version:           18.09.1
 API version:       1.39
 Go version:        go1.10.6
 Git commit:        4c52b90
 Built:             Wed Jan  9 19:33:12 2019
 OS/Arch:           darwin/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.1
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.6
  Git commit:       4c52b90
  Built:            Wed Jan  9 19:41:49 2019
  OS/Arch:          linux/amd64
  Experimental:     false
```

### Get Docker Information - All Details
```
$ docker info
Containers: 3
 Running: 0
 Paused: 0
 Stopped: 3
Images: 2
Server Version: 18.09.1
. . .
```

### Test Docker Installation
This will try to run a 'hello-world' docker Image. If available, it is run. Else, it is downloaded from **Docker Hub** and run.

```
$ docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
```

### List Docker Images

```
$ docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        2 weeks ago         1.84kB
ubuntu              latest              1d9c17228a9e        2 weeks ago         86.7MB

$ docker image ls
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        2 weeks ago         1.84kB
ubuntu              latest              1d9c17228a9e        2 weeks ago         86.7MB
```
### List Docker Containers
Containers are spawned when ```docker run``` is called on a Docker Image. 

```
$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
This shows that there are no running containers.

#### Show all containers (Even exited ones)
```
$ docker container ls --all
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
d1090cb3381d        hello-world         "/hello"            About an hour ago   Exited (0) About an hour ago                       flamboyant_sanderson
```

#### Just show the ID of the container
```
$ docker container ls -aq
d1090cb3381d
```

### Docker Help
#### List all docker commands
```
$ docker

Usage:	docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/Users/subramanyans/.docker")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
. . .
```

#### List Help for a particular command
```
$ docker run --help

Usage:	docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
      --add-host list                  Add a custom host-to-IP mapping (host:ip)
  -a, --attach list                    Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16            Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
      --blkio-weight-device list       Block IO weight (relative device weight) (default [])
      --cap-add list                   Add Linux capabilities

```
### Docker Pull
Pull an image or a repository from a registry

```
$ docker pull alpine

Using default tag: latest
latest: Pulling from library/alpine
cd784148e348: Pull complete 
Digest: sha256:46e71df1e5191ab8b8034c5189e325258ec44ea739bba1e5645cff83c9048ff1
Status: Downloaded newer image for alpine:latest
```

```
$ docker images -a

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        2 weeks ago         1.84kB
ubuntu              latest              1d9c17228a9e        2 weeks ago         86.7MB
alpine              latest              3f53bb00af94        3 weeks ago         4.41MB
```

### Docker Run
#### Run Docker image and get output
This commands runs the image and creates a container. Runs the given command in the container, fetches the output and displayes in docker client.

```
$ docker run alpine ls -l
total 52
drwxr-xr-x    2 root     root          4096 Dec 20 22:25 bin
drwxr-xr-x    5 root     root           340 Jan 16 06:19 dev
drwxr-xr-x    1 root     root          4096 Jan 16 06:19 etc
drwxr-xr-x    2 root     root          4096 Dec 20 22:25 home
drwxr-xr-x    5 root     root          4096 Dec 20 22:25 lib
drwxr-xr-x    5 root     root          4096 Dec 20 22:25 media
```

This command exits after running.

#### Run a command in an interactive terminal
Running the run command with the -it flags attaches us to an interactive tty in the container. Now you can run as many commands in the container as you want

```
$ docker run -it alpine /bin/sh
/ # pwd
/
/ # ls -l
total 52
drwxr-xr-x    2 root     root          4096 Dec 20 22:25 bin
drwxr-xr-x    5 root     root           360 Jan 16 06:23 dev
drwxr-xr-x    1 root     root          4096 Jan 16 06:23 etc
drwxr-xr-x    2 root     root          4096 Dec 20 22:25 home
drwxr-xr-x    5 root     root          4096 Dec 20 22:25 lib
. . .
```

### Display Docker containers
```
$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
beb8272e93b4        alpine              "/bin/sh"           58 seconds ago      Up 57 seconds                           infallible_dijkstra

$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                      PORTS               NAMES
beb8272e93b4        alpine              "/bin/sh"           About a minute ago   Up About a minute                               infallible_dijkstra
25525151651d        alpine              "/bin/bash"         About a minute ago   Created                                         reverent_mirzakhani
1eefb38cfa61        alpine              "ls -l"             5 minutes ago        Exited (0) 5 minutes ago                        upbeat_hoover
eb990852a94d        ubuntu              "bash"              30 minutes ago       Exited (0) 9 minutes ago                        confident_albattani
9328e8d0c172        ubuntu              "bash"              31 minutes ago       Exited (0) 30 minutes ago                       distracted_meninsky
fa632ffd8e14        hello-world         "/hello"            32 minutes ago       Exited (0) 32 minutes ago                       eloquent_rubin
7518bfa8ed33        ubuntu              "bash"              32 minutes ago       Exited (0) 32 minutes ago                       elegant_heyrovsky
08b4e146e0c8        ubuntu              "/bin/bash"         33 minutes ago       Exited (0) 32 minutes ago                       kind_bardeen
```

#### Similar commands
```ps``` lists Docker processes

```
$ docker ps
$ docker ps -a
```

### Terminology

#### Images
The file system and configuration of our application which are used to create containers. 

To find out more about a Docker image, run ```docker inspect alpine```. 

In the demo above, you used the ```docker pull``` command to download the alpine image. When you executed the command ```docker run hello-world```, it also did a docker pull behind the scenes to download the hello-world image.


#### Containers
Running instances of Docker images — containers run the actual applications. 

A container includes an application and all of its dependencies. It shares the kernel with other containers, and runs as an isolated process in user space on the host OS. 

You created a container using ```docker run``` which you did using the alpine image that you downloaded. A list of running containers can be seen using the ```docker ps``` command.

#### Docker daemon
The background service running on the host that manages building, running and distributing Docker containers.

#### Docker client
The command line tool that allows the user to interact with the Docker daemon.

#### Docker Store
A registry of Docker images, where you can find trusted and enterprise ready containers, plugins, and Docker editions.