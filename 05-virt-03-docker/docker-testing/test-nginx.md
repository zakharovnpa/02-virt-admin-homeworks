# Практическая часть Задачи №1
## 
### Запускаем контейнер на базе скачанного образа nginx
#### 1. Запуск контейнера nginx
```bash
root@server1:~# docker run --name=0f23177d18fc -p 80:80 -d nginx
47d7f94da2d2b61acaf70a9a0af1cb937a1a5774498a7619823a24d0cbd9f989
```
#### 2. Подключение к серверу на порт 80 и проверка его работоспособности
```bash
root@server1:~# telnet 127.0.0.1 80
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
```
#### 3. Вводим произвольный набор знаков
```bash
fmsfgbm
```
#### 4. Ответ сервера
```bash
HTTP/1.1 400 Bad Request
Server: nginx/1.21.4
Date: Mon, 13 Dec 2021 08:28:43 GMT
Content-Type: text/html
Content-Length: 157
Connection: close

<html>
<head><title>400 Bad Request</title></head>
<body>
<center><h1>400 Bad Request</h1></center>
<hr><center>nginx/1.21.4</center>
</body>
</html>
Connection closed by foreign host.
root@server1:~# 
root@server1:~# 

```
#### 5. Входим в контейнер и запускаем bash
```bash
root@server1:~# docker exec -it 47d7f94da2d2 bash
root@47d7f94da2d2:/# 

```
#### 6. Првоеряем конфигурацию сервер
```bash
root@47d7f94da2d2:/# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
root@47d7f94da2d2:/# 

```
#### 7. Проверяем полную конфигурацию. Ищем стартовую страницу
```bash
root@47d7f94da2d2:/# nginx -T
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
# configuration file /etc/nginx/nginx.conf:

user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}

# configuration file /etc/nginx/mime.types:

types {
    text/html                                        html htm shtml;
    text/css                                         css;
    text/xml                                         xml;
    image/gif                                        gif;
    image/jpeg                                       jpeg jpg;
    application/javascript                           js;
    application/atom+xml                             atom;
    application/rss+xml                              rss;

    text/mathml                                      mml;
    text/plain                                       txt;
    text/vnd.sun.j2me.app-descriptor                 jad;
    text/vnd.wap.wml                                 wml;
    text/x-component                                 htc;

    image/avif                                       avif;
    image/png                                        png;
    image/svg+xml                                    svg svgz;
    image/tiff                                       tif tiff;
    image/vnd.wap.wbmp                               wbmp;
    image/webp                                       webp;
    image/x-icon                                     ico;
    image/x-jng                                      jng;
    image/x-ms-bmp                                   bmp;

    font/woff                                        woff;
    font/woff2                                       woff2;

    application/java-archive                         jar war ear;
    application/json                                 json;
    application/mac-binhex40                         hqx;
    application/msword                               doc;
    application/pdf                                  pdf;
    application/postscript                           ps eps ai;
    application/rtf                                  rtf;
    application/vnd.apple.mpegurl                    m3u8;
    application/vnd.google-earth.kml+xml             kml;
    application/vnd.google-earth.kmz                 kmz;
    application/vnd.ms-excel                         xls;
    application/vnd.ms-fontobject                    eot;
    application/vnd.ms-powerpoint                    ppt;
    application/vnd.oasis.opendocument.graphics      odg;
    application/vnd.oasis.opendocument.presentation  odp;
    application/vnd.oasis.opendocument.spreadsheet   ods;
    application/vnd.oasis.opendocument.text          odt;
    application/vnd.openxmlformats-officedocument.presentationml.presentation
                                                     pptx;
    application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
                                                     xlsx;
    application/vnd.openxmlformats-officedocument.wordprocessingml.document
                                                     docx;
    application/vnd.wap.wmlc                         wmlc;
    application/wasm                                 wasm;
    application/x-7z-compressed                      7z;
    application/x-cocoa                              cco;
    application/x-java-archive-diff                  jardiff;
    application/x-java-jnlp-file                     jnlp;
    application/x-makeself                           run;
    application/x-perl                               pl pm;
    application/x-pilot                              prc pdb;
    application/x-rar-compressed                     rar;
    application/x-redhat-package-manager             rpm;
    application/x-sea                                sea;
    application/x-shockwave-flash                    swf;
    application/x-stuffit                            sit;
    application/x-tcl                                tcl tk;
    application/x-x509-ca-cert                       der pem crt;
    application/x-xpinstall                          xpi;
    application/xhtml+xml                            xhtml;
    application/xspf+xml                             xspf;
    application/zip                                  zip;

    application/octet-stream                         bin exe dll;
    application/octet-stream                         deb;
    application/octet-stream                         dmg;
    application/octet-stream                         iso img;
    application/octet-stream                         msi msp msm;

    audio/midi                                       mid midi kar;
    audio/mpeg                                       mp3;
    audio/ogg                                        ogg;
    audio/x-m4a                                      m4a;
    audio/x-realaudio                                ra;

    video/3gpp                                       3gpp 3gp;
    video/mp2t                                       ts;
    video/mp4                                        mp4;
    video/mpeg                                       mpeg mpg;
    video/quicktime                                  mov;
    video/webm                                       webm;
    video/x-flv                                      flv;
    video/x-m4v                                      m4v;
    video/x-mng                                      mng;
    video/x-ms-asf                                   asx asf;
    video/x-ms-wmv                                   wmv;
    video/x-msvideo                                  avi;
}

# configuration file /etc/nginx/conf.d/default.conf:
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}


root@47d7f94da2d2:/# 

```
#### 8. Стартовая страница лежит здесь ` /usr/share/nginx/html/index.html `
```bash
root@47d7f94da2d2:/usr/share/nginx/html# cat index.html 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@47d7f94da2d2:/usr/share/nginx/html# 

```
#### 9. Подключаем общие каталоги (Volume) для клпирования файлов из хостовой системы в запущенный контейнер
```bash
root@server1:~# 
root@server1:~# docker run -v /root/nginx:/usr/share/nginx/html --name=47d7f94da2d2 -d nginx
a9b20fc2235fad042fc8e7750b38153d516cc2aef005ca7f673ea973474cbc83
root@server1:~# 
root@server1:~# 
```
```bash
root@server1:~# ls -l
total 8
drwxr-xr-x 3 root root 4096 Dec  8 16:34 build
drwxr-xr-x 2 root root 4096 Dec 13 09:13 nginx
root@server1:~# 
```
```bash
root@server1:~# cd nginx/
root@server1:~/nginx# 
root@server1:~/nginx# ls -l
total 4
-rw-r--r-- 1 root root 91 Dec 13 09:13 index.html
root@server1:~/nginx# 
```
```bash
root@server1:~/nginx# cat index.html 
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
root@server1:~/nginx# 
root@server1:~/nginx# cd
root@server1:~# 
```
#### 10. Входим в контейнер 
```bash
root@server1:~# docker exec -it 47d7f94da2d2 bash
root@a9b20fc2235f:/# 
root@a9b20fc2235f:/# cd /usr/share/nginx/html/
root@a9b20fc2235f:/usr/share/nginx/html# 
root@a9b20fc2235f:/usr/share/nginx/html# ls -l
total 4
-rw-r--r-- 1 root root 91 Dec 13 09:13 index.html
root@a9b20fc2235f:/usr/share/nginx/html# 
root@a9b20fc2235f:/usr/share/nginx/html# cat index.html 
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```
```bash

root@a9b20fc2235f:/usr/share/nginx/html# cat index.html 
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
root@a9b20fc2235f:/usr/share/nginx/html# 
root@a9b20fc2235f:/usr/share/nginx/html# 
root@a9b20fc2235f:/usr/share/nginx/html# cd 
root@a9b20fc2235f:~# 
root@a9b20fc2235f:~# exit
exit
root@server1:~# 
```

```bash
root@server1:~# type curl
curl is /usr/bin/curl
root@server1:~# 
root@server1:~# curl -X GET 'http://127.0.0.1:80'
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@server1:~# 
```

```bash
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                               NAMES
a9b20fc2235f   nginx     "/docker-entrypoint.…"   34 minutes ago      Up 34 minutes      80/tcp                              47d7f94da2d2
47d7f94da2d2   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   0f23177d18fc
root@server1:~# 
root@server1:~# docker run -h
flag needs an argument: 'h' in -h
See 'docker run --help'.
root@server1:~# 
root@server1:~# docker run --help

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
      --add-host list                  Add a custom host-to-IP mapping (host:ip)
  -a, --attach list                    Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16            Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
      --blkio-weight-device list       Block IO weight (relative device weight) (default [])
      --cap-add list                   Add Linux capabilities
      --cap-drop list                  Drop Linux capabilities
      --cgroup-parent string           Optional parent cgroup for the container
      --cgroupns string                Cgroup namespace to use (host|private)
                                       'host':    Run the container in the Docker host's cgroup namespace
                                       'private': Run the container in its own private cgroup namespace
                                       '':        Use the cgroup namespace as configured by the
                                                  default-cgroupns-mode option on the daemon (default)
      --cidfile string                 Write the container ID to the file
      --cpu-period int                 Limit CPU CFS (Completely Fair Scheduler) period
      --cpu-quota int                  Limit CPU CFS (Completely Fair Scheduler) quota
      --cpu-rt-period int              Limit CPU real-time period in microseconds
      --cpu-rt-runtime int             Limit CPU real-time runtime in microseconds
  -c, --cpu-shares int                 CPU shares (relative weight)
      --cpus decimal                   Number of CPUs
      --cpuset-cpus string             CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string             MEMs in which to allow execution (0-3, 0,1)
  -d, --detach                         Run container in background and print container ID
      --detach-keys string             Override the key sequence for detaching a container
      --device list                    Add a host device to the container
      --device-cgroup-rule list        Add a rule to the cgroup allowed devices list
      --device-read-bps list           Limit read rate (bytes per second) from a device (default [])
      --device-read-iops list          Limit read rate (IO per second) from a device (default [])
      --device-write-bps list          Limit write rate (bytes per second) to a device (default [])
      --device-write-iops list         Limit write rate (IO per second) to a device (default [])
      --disable-content-trust          Skip image verification (default true)
      --dns list                       Set custom DNS servers
      --dns-option list                Set DNS options
      --dns-search list                Set custom DNS search domains
      --domainname string              Container NIS domain name
      --entrypoint string              Overwrite the default ENTRYPOINT of the image
  -e, --env list                       Set environment variables
      --env-file list                  Read in a file of environment variables
      --expose list                    Expose a port or a range of ports
      --gpus gpu-request               GPU devices to add to the container ('all' to pass all GPUs)
      --group-add list                 Add additional groups to join
      --health-cmd string              Command to run to check health
      --health-interval duration       Time between running the check (ms|s|m|h) (default 0s)
      --health-retries int             Consecutive failures needed to report unhealthy
      --health-start-period duration   Start period for the container to initialize before starting health-retries countdown (ms|s|m|h) (default 0s)
      --health-timeout duration        Maximum time to allow one check to run (ms|s|m|h) (default 0s)
      --help                           Print usage
  -h, --hostname string                Container host name
      --init                           Run an init inside the container that forwards signals and reaps processes
  -i, --interactive                    Keep STDIN open even if not attached
      --ip string                      IPv4 address (e.g., 172.30.100.104)
      --ip6 string                     IPv6 address (e.g., 2001:db8::33)
      --ipc string                     IPC mode to use
      --isolation string               Container isolation technology
      --kernel-memory bytes            Kernel memory limit
  -l, --label list                     Set meta data on a container
      --label-file list                Read in a line delimited file of labels
      --link list                      Add link to another container
      --link-local-ip list             Container IPv4/IPv6 link-local addresses
      --log-driver string              Logging driver for the container
      --log-opt list                   Log driver options
      --mac-address string             Container MAC address (e.g., 92:d0:c6:0a:29:33)
  -m, --memory bytes                   Memory limit
      --memory-reservation bytes       Memory soft limit
      --memory-swap bytes              Swap limit equal to memory plus swap: '-1' to enable unlimited swap
      --memory-swappiness int          Tune container memory swappiness (0 to 100) (default -1)
      --mount mount                    Attach a filesystem mount to the container
      --name string                    Assign a name to the container
      --network network                Connect a container to a network
      --network-alias list             Add network-scoped alias for the container
      --no-healthcheck                 Disable any container-specified HEALTHCHECK
      --oom-kill-disable               Disable OOM Killer
      --oom-score-adj int              Tune host's OOM preferences (-1000 to 1000)
      --pid string                     PID namespace to use
      --pids-limit int                 Tune container pids limit (set -1 for unlimited)
      --platform string                Set platform if server is multi-platform capable
      --privileged                     Give extended privileges to this container
  -p, --publish list                   Publish a container's port(s) to the host
  -P, --publish-all                    Publish all exposed ports to random ports
      --pull string                    Pull image before running ("always"|"missing"|"never") (default "missing")
      --read-only                      Mount the container's root filesystem as read only
      --restart string                 Restart policy to apply when a container exits (default "no")
      --rm                             Automatically remove the container when it exits
      --runtime string                 Runtime to use for this container
      --security-opt list              Security Options
      --shm-size bytes                 Size of /dev/shm
      --sig-proxy                      Proxy received signals to the process (default true)
      --stop-signal string             Signal to stop a container (default "SIGTERM")
      --stop-timeout int               Timeout (in seconds) to stop a container
      --storage-opt list               Storage driver options for the container
      --sysctl map                     Sysctl options (default map[])
      --tmpfs list                     Mount a tmpfs directory
  -t, --tty                            Allocate a pseudo-TTY
      --ulimit ulimit                  Ulimit options (default [])
  -u, --user string                    Username or UID (format: <name|uid>[:<group|gid>])
      --userns string                  User namespace to use
      --uts string                     UTS namespace to use
  -v, --volume list                    Bind mount a volume
      --volume-driver string           Optional volume driver for the container
      --volumes-from list              Mount volumes from the specified container(s)
  -w, --workdir string                 Working directory inside the container
root@server1:~# 
root@server1:~# 
```

```bash
root@server1:~# docker run -v /root/nginx:/usr/share/nginx/html --name=Alfa -d nginx
c1de7e926d1bbd26fae982e6bc004b9ff6938b7a4be8e13630d7068294c36f52
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                               NAMES
c1de7e926d1b   nginx     "/docker-entrypoint.…"   7 seconds ago       Up 6 seconds       80/tcp                              Alfa
a9b20fc2235f   nginx     "/docker-entrypoint.…"   39 minutes ago      Up 39 minutes      80/tcp                              47d7f94da2d2
47d7f94da2d2   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   0f23177d18fc
root@server1:~# 
```

```bash
root@server1:~# docker stop Alfa
Alfa
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                               NAMES
a9b20fc2235f   nginx     "/docker-entrypoint.…"   40 minutes ago      Up 40 minutes      80/tcp                              47d7f94da2d2
47d7f94da2d2   nginx     "/docker-entrypoint.…"   About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   0f23177d18fc
root@server1:~# 
```

```bash
root@server1:~# docker stop 47d7f94da2d2
47d7f94da2d2
root@server1:~# 
```

```bash
root@server1:~# curl -X GET 'http://127.0.0.1:80'
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@server1:~# 
root@server1:~# 
```

```bash
root@server1:~# docker stop 0f23177d18fc
0f23177d18fc
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@server1:~# 
root@server1:~# 
```

```bash
root@server1:~# docker run -v /root/nginx:/usr/share/nginx/volume --name=Alfa -d nginx
docker: Error response from daemon: Conflict. The container name "/Alfa" is already in use by container "c1de7e926d1bbd26fae982e6bc004b9ff6938b7a4be8e13630d7068294c36f52". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
root@server1:~# 
```

```bash
root@server1:~# docker run -v /root/nginx:/usr/share/nginx/volume --name=Betta -d nginx
24c9d73fb32900254c9dada154d253785f5edc7b98a855f5dc014c6f0cfe87e1
root@server1:~# 
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
24c9d73fb329   nginx     "/docker-entrypoint.…"   7 seconds ago   Up 6 seconds   80/tcp    Betta
root@server1:~# 
root@server1:~# curl -X GET 'http://127.0.0.1:80'
curl: (7) Failed to connect to 127.0.0.1 port 80: Connection refused
root@server1:~# 
root@server1:~# 
root@server1:~# curl -X GET 'http://127.0.0.1:80'
curl: (7) Failed to connect to 127.0.0.1 port 80: Connection refused
root@server1:~# 
root@server1:~# docker stop
"docker stop" requires at least 1 argument.
See 'docker stop --help'.

Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]

Stop one or more running containers
root@server1:~# 
root@server1:~# docker stop 24c9d73fb329
24c9d73fb329
root@server1:~# 
```

```bash
root@server1:~# docker run -v /root/nginx:/usr/share/nginx/volume --name=Gamma -p 80:80 -d nginx
55b1e2b3c55daea218af64aa7b83e574d7c2b72095e200b3116ab4fe792b6e3d
root@server1:~# 
root@server1:~# 
root@server1:~# curl -X GET 'http://127.0.0.1:80'
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@server1:~# 
root@server1:~# 
```

```bash
root@server1:~# cd nginx/
root@server1:~/nginx# 
root@server1:~/nginx# ls -l
total 4
-rw-r--r-- 1 root root 91 Dec 13 09:13 index.html
root@server1:~/nginx# 
root@server1:~/nginx# cat index.html 
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
root@server1:~/nginx# 
root@server1:~/nginx# 
```

```bash
root@server1:~/nginx# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                               NAMES
55b1e2b3c55d   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   Gamma
root@server1:~/nginx# 
root@server1:~/nginx# docker exec -it Gamma ls -l /usr/share/nginx/volume
total 4
-rw-r--r-- 1 root root 91 Dec 13 09:13 index.html
root@server1:~/nginx# 
root@server1:~/nginx# docker exec -it Gamma cat index.html
cat: index.html: No such file or directory
root@server1:~/nginx# 
```

```bash
root@server1:~/nginx# docker exec -it Gamma cp /usr/share/nginx/volume/index.html /usr/share/nginx/html
root@server1:~/nginx# 
root@server1:~/nginx# curl -X GET 'http://127.0.0.1:80'
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
root@server1:~/nginx# 
root@server1:~/nginx# 
root@server1:~/nginx# 


```
1. 
```bash
root@server1:~/nginx# docker exec -it Gamma bash
root@55b1e2b3c55d:/# 
root@55b1e2b3c55d:/# 


```
1. 
```bash
```
1. 
```bash

```
####  Конфигурация веб-сервера
```bash
root@47d7f94da2d2:/usr/share/nginx/html# nginx -V
nginx version: nginx/1.21.4
built by gcc 10.2.1 20210110 (Debian 10.2.1-6) 
built with OpenSSL 1.1.1k  25 Mar 2021
TLS SNI support enabled
configure arguments: 
--prefix=/etc/nginx 
--sbin-path=/usr/sbin/nginx 
--modules-path=/usr/lib/nginx/modules 
--conf-path=/etc/nginx/nginx.conf
--error-log-path=/var/log/nginx/error.log 
--http-log-path=/var/log/nginx/access.log 
--pid-path=/var/run/nginx.pid 
--lock-path=/var/run/nginx.lock 
--http-client-body-temp-path=/var/cache/nginx/client_temp 
--http-proxy-temp-path=/var/cache/nginx/proxy_temp 
--http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp 
--http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp 
--http-scgi-temp-path=/var/cache/nginx/scgi_temp 
--user=nginx 
--group=nginx 
--with-compat 
--with-file-aio 
--with-threads 
--with-http_addition_module 
--with-http_auth_request_module 
--with-http_dav_module 
--with-http_flv_module 
--with-http_gunzip_module 
--with-http_gzip_static_module 
--with-http_mp4_module 
--with-http_random_index_module 
--with-http_realip_module 
--with-http_secure_link_module 
--with-http_slice_module 
--with-http_ssl_module 
--with-http_stub_status_module 
--with-http_sub_module 
--with-http_v2_module 
--with-mail 
--with-mail_ssl_module 
--with-stream 
--with-stream_realip_module 
--with-stream_ssl_module 
--with-stream_ssl_preread_module 
--with-cc-opt='-g -O2 -ffile-prefix-map=/data/builder/debuild/nginx-1.21.4/debian/debuild-base/nginx-1.21.4=. -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie'

```
