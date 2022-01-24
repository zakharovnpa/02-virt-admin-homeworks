#
##
### На ВМ Vagrant-Betta

```bash
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
```bash
root@server1:~# docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:cc15c5b292d8525effc0f89cb299f1804f3a725c8d05e158653a563f15e4f685
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
```
```bash
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@server1:~# 
root@server1:~# 
```
```bash
root@server1:~# docker ls
docker: 'ls' is not a docker command.
See 'docker --help'
root@server1:~# 
```
```bash
root@server1:~# docker image ls
REPOSITORY            TAG       IMAGE ID       CREATED        SIZE
zakharovnpa/ansible   8.12.21   06b6ca73286e   3 days ago     227MB
alpine                3.14      0a97eee8041e   4 weeks ago    5.61MB
hello-world           latest    feb5d9fea6a5   2 months ago   13.3kB
root@server1:~# 
root@server1:~# 
root@server1:~# docker ?
docker: '?' is not a docker command.
See 'docker --help'
root@server1:~# 
```
```bash
root@server1:~# docker --help

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/root/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/root/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/root/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  app*        Docker App (Docker Inc., v0.9.1-beta3)
  builder     Manage builds
  buildx*     Build with BuildKit (Docker Inc., v0.6.3-docker)
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  scan*       Docker Scan (Docker Inc., v0.9.0)
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.

To get more help with docker, check out our guides at https://docs.docker.com/go/guides/
root@server1:~# 
root@server1:~# 
```
####
```bash
root@server1:~# docker image ls
REPOSITORY            TAG       IMAGE ID       CREATED        SIZE
zakharovnpa/ansible   8.12.21   06b6ca73286e   3 days ago     227MB
alpine                3.14      0a97eee8041e   4 weeks ago    5.61MB
hello-world           latest    feb5d9fea6a5   2 months ago   13.3kB
root@server1:~# 
root@server1:~# 
```
####
```bash
root@server1:~# docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
7b1a6ab2e44d: Pull complete 
Digest: sha256:626ffe58f6e7566e00254b638eb7e0f3b11d4da9675088f4781a50ae288f3322
Status: Downloaded newer image for ubuntu:latest
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
root@42f6cd1a71e7:/# 
```
#### 
```bash
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# dmesg
dmesg: read kernel buffer failed: Operation not permitted
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# type dmesg
dmesg is hashed (/usr/bin/dmesg)
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# pwd
/
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# ls -lha
total 56K
drwxr-xr-x   1 root root 4.0K Dec 12 15:13 .
drwxr-xr-x   1 root root 4.0K Dec 12 15:13 ..
-rwxr-xr-x   1 root root    0 Dec 12 15:13 .dockerenv
lrwxrwxrwx   1 root root    7 Oct  6 16:47 bin -> usr/bin
drwxr-xr-x   2 root root 4.0K Apr 15  2020 boot
drwxr-xr-x   5 root root  360 Dec 12 15:13 dev
drwxr-xr-x   1 root root 4.0K Dec 12 15:13 etc
drwxr-xr-x   2 root root 4.0K Apr 15  2020 home
lrwxrwxrwx   1 root root    7 Oct  6 16:47 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Oct  6 16:47 lib32 -> usr/lib32
lrwxrwxrwx   1 root root    9 Oct  6 16:47 lib64 -> usr/lib64
lrwxrwxrwx   1 root root   10 Oct  6 16:47 libx32 -> usr/libx32
drwxr-xr-x   2 root root 4.0K Oct  6 16:47 media
drwxr-xr-x   2 root root 4.0K Oct  6 16:47 mnt
drwxr-xr-x   2 root root 4.0K Oct  6 16:47 opt
dr-xr-xr-x 156 root root    0 Dec 12 15:13 proc
drwx------   2 root root 4.0K Oct  6 16:58 root
drwxr-xr-x   5 root root 4.0K Oct  6 16:58 run
lrwxrwxrwx   1 root root    8 Oct  6 16:47 sbin -> usr/sbin
drwxr-xr-x   2 root root 4.0K Oct  6 16:47 srv
dr-xr-xr-x  13 root root    0 Dec 12 15:13 sys
drwxrwxrwt   2 root root 4.0K Oct  6 16:58 tmp
drwxr-xr-x  13 root root 4.0K Oct  6 16:47 usr
drwxr-xr-x  11 root root 4.0K Oct  6 16:58 var
root@42f6cd1a71e7:/# 
```
####
```bash
root@42f6cd1a71e7:/# uptime
 15:14:38 up 13 min,  0 users,  load average: 0.10, 0.08, 0.07
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# docker ps        
bash: docker: command not found
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# type docker
bash: type: docker: not found
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# ip add
bash: ip: command not found
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# ps -aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.3   4228  3488 pts/0    Ss   15:13   0:00 bash
root          14  0.0  0.2   5896  2776 pts/0    R+   15:18   0:00 ps -aux
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# top

top - 15:18:58 up 17 min,  0 users,  load average: 0.00, 0.03, 0.04
Tasks:   2 total,   1 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :    981.3 total,    245.3 free,    161.1 used,    574.8 buff/cache
MiB Swap:    980.0 total,    980.0 free,      0.0 used.    666.4 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                                                
     15 root      20   0    6128   3284   2756 R   0.3   0.3   0:00.01 top                                                                                                                                    
      1 root      20   0    4228   3488   2928 S   0.0   0.3   0:00.07 bash                                                                                                                                   


root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# type top
top is hashed (/usr/bin/top)
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# man top
This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, including manpages, you can run the 'unminimize'
command. You will still need to ensure the 'man-db' package is installed.
root@42f6cd1a71e7:/# 
```
```bash
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 
root@42f6cd1a71e7:/# 


```
