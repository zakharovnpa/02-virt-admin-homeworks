## Ход выполнения Задачи №1
### Для решения задачи необходимо было создать новый образ с заявленными изменениями из образа nginx
#### Создаем Dockerfile и файл index.html
```bash
# Манифест Docker образа.

FROM nginx

# Заменяем дефолтную страницу nginx соответствующей веб-приложению
RUN rm -rf /usr/share/nginx/html/*

# Копируем новый файл index.html в каталог на будующем образе
COPY ./html/index.html /usr/share/nginx/html

```
#### Файл index.html
```bash
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>

```
#### Запускаем создание образа
```bash
root@server1:~/build/nginx# docker build -t zakharovnpa/nginx:13.12.21 .
Sending build context to Docker daemon  4.608kB
Step 1/3 : FROM nginx
 ---> f652ca386ed1
Step 2/3 : RUN rm -rf /usr/share/nginx/html/*
 ---> Running in 58d18923e45b
Removing intermediate container 58d18923e45b
 ---> 993637835b2b
Step 3/3 : COPY ./html/index.html /usr/share/nginx/html
 ---> 4b8b755d634a
Successfully built 4b8b755d634a
Successfully tagged zakharovnpa/nginx:13.12.21
```
#### Образ создан
```bash
root@server1:~/build/nginx# docker image ls
REPOSITORY            TAG        IMAGE ID       CREATED         SIZE
zakharovnpa/nginx     13.12.21   4b8b755d634a   9 seconds ago   141MB

```
#### Запускаем контейнер
```bash
root@server1:~/build/nginx# docker run --name=Alfa-nginx -p 80:80 -d zakharovnpa/nginx:13.12.21
0a2533d58415906a2c34fa8bbf0833112434192a286ef2e46b87fde3c085db90
root@server1:~/build/nginx# 
root@server1:~/build/nginx# 
root@server1:~/build/nginx# docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS          PORTS                               NAMES
0a2533d58415   zakharovnpa/nginx:13.12.21   "/docker-entrypoint.…"   14 seconds ago   Up 12 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   Alfa-nginx

```
#### Проеряем ответ сервера
```bash
root@server1:~/build/nginx# curl -X GET 'http://127.0.0.1:80'
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>

```
#### Ответ сервера в браузере
![i-am-devops-engeneer](/05-virt-03-docker/img/i-am-devops-engeneer.png)
