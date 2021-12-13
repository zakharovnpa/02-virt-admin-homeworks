## Практическая часть выполнения Задачи №3

### Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тэгом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера;
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```;
- Добавьте еще один файл в папку ```/data``` на хостовой машине;
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

**Ответ:**
Как работать с Volume

##### Скачали образы
```bash
root@server1:~/build# docker pull centos:7
7: Pulling from library/centos
2d473b07cdd5: Pull complete 
Digest: sha256:9d4bcbbb213dfd745b58be38b13b996ebb5ac315fe75711bd618426a630e0987
Status: Downloaded newer image for centos:7
docker.io/library/centos:7
root@server1:~/build# 
root@server1:~/build# docker image ls
REPOSITORY            TAG        IMAGE ID       CREATED        SIZE
centos                7          eeb6ee3f44bd   2 months ago   204MB

```
##### Создали файлы Dockerfile для [Centos](https://hub.docker.com/_/centos) и Debioan 
```ps
#Dockerfile for Centos
FROM centos:7

ENV container docker

RUN yum -y install httpd; yum clean all; systemctl enable httpd.service
EXPOSE 80
CMD ["/usr/sbin/init"]
VOLUME [ "/tmp/data" ]
CMD ["/usr/sbin/init"]

```
```bash
#Dockerfile for Debian
FROM debian

ENV container docker

RUN apt install httpd; systemctl enable httpd.service
EXPOSE 80
CMD ["/usr/sbin/init"]
VOLUME [ "/tmp/data" ]
CMD ["/usr/sbin/init"]

```
#### Запускаем сборку нового образа Centos
```ps
root@server1:~/build/centos7# docker build -t zakharovnpa/centos7:001 .
Sending build context to Docker daemon  2.048kB
Step 1/7 : FROM centos:7
 ---> eeb6ee3f44bd
Step 2/7 : ENV container docker
 ---> Running in 089c609f6c2e
Removing intermediate container 089c609f6c2e
 ---> 9c8d761e2607
Step 3/7 : RUN yum -y install httpd; yum clean all; systemctl enable httpd.service
 ---> Running in 400ee7893a22
Loaded plugins: fastestmirror, ovl
Determining fastest mirrors
 * base: mirror.docker.ru
 * extras: mirror.docker.ru
 * updates: mirror.corbina.net
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-97.el7.centos.2 will be installed
--> Processing Dependency: httpd-tools = 2.4.6-97.el7.centos.2 for package: httpd-2.4.6-97.el7.centos.2.x86_64
--> Processing Dependency: system-logos >= 7.92.1-1 for package: httpd-2.4.6-97.el7.centos.2.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-97.el7.centos.2.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.6-97.el7.centos.2.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.6-97.el7.centos.2.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.4.8-7.el7 will be installed
---> Package apr-util.x86_64 0:1.5.2-6.el7 will be installed
---> Package centos-logos.noarch 0:70.0.6-3.el7.centos will be installed
---> Package httpd-tools.x86_64 0:2.4.6-97.el7.centos.2 will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package           Arch        Version                       Repository    Size
================================================================================
Installing:
 httpd             x86_64      2.4.6-97.el7.centos.2         updates      2.7 M
Installing for dependencies:
 apr               x86_64      1.4.8-7.el7                   base         104 k
 apr-util          x86_64      1.5.2-6.el7                   base          92 k
 centos-logos      noarch      70.0.6-3.el7.centos           base          21 M
 httpd-tools       x86_64      2.4.6-97.el7.centos.2         updates       94 k
 mailcap           noarch      2.1.41-2.el7                  base          31 k

Transaction Summary
================================================================================
Install  1 Package (+5 Dependent packages)

Total download size: 24 M
Installed size: 32 M
Downloading packages:
warning: /var/cache/yum/x86_64/7/base/packages/apr-util-1.5.2-6.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
Public key for apr-util-1.5.2-6.el7.x86_64.rpm is not installed
Public key for httpd-tools-2.4.6-97.el7.centos.2.x86_64.rpm is not installed
--------------------------------------------------------------------------------
Total                                              2.1 MB/s |  24 MB  00:11     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-9.2009.0.el7.centos.x86_64 (@CentOS)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : apr-1.4.8-7.el7.x86_64                                       1/6 
  Installing : apr-util-1.5.2-6.el7.x86_64                                  2/6 
  Installing : httpd-tools-2.4.6-97.el7.centos.2.x86_64                     3/6 
  Installing : centos-logos-70.0.6-3.el7.centos.noarch                      4/6 
  Installing : mailcap-2.1.41-2.el7.noarch                                  5/6 
  Installing : httpd-2.4.6-97.el7.centos.2.x86_64                           6/6 
  Verifying  : httpd-2.4.6-97.el7.centos.2.x86_64                           1/6 
  Verifying  : httpd-tools-2.4.6-97.el7.centos.2.x86_64                     2/6 
  Verifying  : mailcap-2.1.41-2.el7.noarch                                  3/6 
  Verifying  : apr-1.4.8-7.el7.x86_64                                       4/6 
  Verifying  : apr-util-1.5.2-6.el7.x86_64                                  5/6 
  Verifying  : centos-logos-70.0.6-3.el7.centos.noarch                      6/6 

Installed:
  httpd.x86_64 0:2.4.6-97.el7.centos.2                                          

Dependency Installed:
  apr.x86_64 0:1.4.8-7.el7                                                      
  apr-util.x86_64 0:1.5.2-6.el7                                                 
  centos-logos.noarch 0:70.0.6-3.el7.centos                                     
  httpd-tools.x86_64 0:2.4.6-97.el7.centos.2                                    
  mailcap.noarch 0:2.1.41-2.el7                                                 

Complete!
Loaded plugins: fastestmirror, ovl
Cleaning repos: base extras updates
Cleaning up list of fastest mirrors
Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service, pointing to /usr/lib/systemd/system/httpd.service.
Removing intermediate container 400ee7893a22
 ---> 0c955d736ab3
Step 4/7 : EXPOSE 80
 ---> Running in bc972d27fdaa
Removing intermediate container bc972d27fdaa
 ---> 3c37aa7cfd0b
Step 5/7 : CMD ["/usr/sbin/init"]
 ---> Running in 3a8a76da38ed
Removing intermediate container 3a8a76da38ed
 ---> 169690a910b6
Step 6/7 : VOLUME [ "/tmp/data" ]
 ---> Running in 9c9e0888b11c
Removing intermediate container 9c9e0888b11c
 ---> b4e9521cc30e
Step 7/7 : CMD ["/usr/sbin/init"]
 ---> Running in c09e1b80691b
Removing intermediate container c09e1b80691b
 ---> 62ad6751e301
Successfully built 62ad6751e301
Successfully tagged zakharovnpa/centos7:001
```
#### Коллекция образов
```ps
root@server1:~/build/centos7# docker image ls
REPOSITORY            TAG        IMAGE ID       CREATED          SIZE
zakharovnpa/centos7   001        62ad6751e301   21 seconds ago   261MB
zakharovnpa/nginx     13.12.21   4b8b755d634a   4 hours ago      141MB
zakharovnpa/ansible   8.12.21    06b6ca73286e   4 days ago       227MB
nginx                 latest     f652ca386ed1   11 days ago      141MB
debian                latest     05d2318291e3   11 days ago      124MB
alpine                3.14       0a97eee8041e   4 weeks ago      5.61MB
ubuntu                latest     ba6acccedd29   8 weeks ago      72.8MB
hello-world           latest     feb5d9fea6a5   2 months ago     13.3kB
centos                7          eeb6ee3f44bd   2 months ago     204MB
centos                latest     5d0da3dc9764   2 months ago     231MB
root@server1:~/build/centos7# 
```
#### Запуск контейнера
```ps
root@server1:~/build/centos7# docker run --name=Toyota -d zakharovnpa/centos7:001
b0146acb57b1fbbe285ef37ef2924edffccdb92be19a336b50764d5f72bd5fea
root@server1:~/build/centos7# 
```
#### Запущенные контейнеры
```ps
root@server1:~/build/centos7# docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED         STATUS         PORTS                               NAMES
b0146acb57b1   zakharovnpa/centos7:001      "/usr/sbin/init"         6 seconds ago   Up 5 seconds   80/tcp                              Toyota
c25089291551   zakharovnpa/nginx:13.12.21   "/docker-entrypoint.…"   2 hours ago     Up 2 hours     0.0.0.0:80->80/tcp, :::80->80/tcp   Alfa-nginx
root@server1:~/build/centos7# 
root@server1:~/build/centos7# 
root@server1:~/build/centos7# docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS          PORTS                               NAMES
b0146acb57b1   zakharovnpa/centos7:001      "/usr/sbin/init"         10 minutes ago   Up 10 minutes   80/tcp                              Toyota
c25089291551   zakharovnpa/nginx:13.12.21   "/docker-entrypoint.…"   2 hours ago      Up 2 hours      0.0.0.0:80->80/tcp, :::80->80/tcp   Alfa-nginx
root@server1:~/build/centos7# 
root@server1:~/build/centos7# 
```
#### Передаем в контейнер команду на запуск оболочки
```ps
root@server1:~/build/centos7# docker exec -it Toyota bash
```
#### Командуем в контейнере
```ps
[root@b0146acb57b1 /]# 
[root@b0146acb57b1 /]# ls -l
total 60
-rw-r--r--   1 root root 12114 Nov 13  2020 anaconda-post.log
lrwxrwxrwx   1 root root     7 Nov 13  2020 bin -> usr/bin
drwxr-xr-x   3 root root  4096 Dec 13 16:12 boot
drwxr-xr-x   5 root root   340 Dec 13 16:14 dev
drwxr-xr-x   1 root root  4096 Dec 13 16:14 etc
drwxr-xr-x   2 root root  4096 Apr 11  2018 home
lrwxrwxrwx   1 root root     7 Nov 13  2020 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Nov 13  2020 lib64 -> usr/lib64
drwxr-xr-x   2 root root  4096 Apr 11  2018 media
drwxr-xr-x   2 root root  4096 Apr 11  2018 mnt
drwxr-xr-x   2 root root  4096 Apr 11  2018 opt
dr-xr-xr-x 160 root root     0 Dec 13 16:14 proc
dr-xr-x---   2 root root  4096 Nov 13  2020 root
drwxr-xr-x   1 root root  4096 Dec 13 16:12 run
lrwxrwxrwx   1 root root     8 Nov 13  2020 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 Apr 11  2018 srv
dr-xr-xr-x  13 root root     0 Dec 13 16:14 sys
drwxrwxrwt   1 root root  4096 Dec 13 16:14 tmp
drwxr-xr-x   1 root root  4096 Nov 13  2020 usr
drwxr-xr-x   1 root root  4096 Dec 13 16:12 var
[root@b0146acb57b1 /]# 
```
#### Проверяем готовность Volume
```ps
[root@b0146acb57b1 /]# cd tmp
[root@b0146acb57b1 tmp]# 
[root@b0146acb57b1 tmp]# ls -l
total 8
drwxr-xr-x 2 root root 4096 Dec 13 16:14 data
-rwx------ 1 root root  836 Nov 13  2020 ks-script-DrRL8A
-rw------- 1 root root    0 Nov 13  2020 yum.log
[root@b0146acb57b1 tmp]# 
[root@b0146acb57b1 tmp]# cd data/
[root@b0146acb57b1 data]# 
[root@b0146acb57b1 data]# 
[root@b0146acb57b1 data]# ls -l
total 0

```
