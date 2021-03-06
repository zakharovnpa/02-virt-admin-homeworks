# Лекция по теме "5.3 Введение. Экосистема, архитектура, жизненный цикл Docker контейнера"

Букатчук Олег

Должность,
Architect DevOps, компания crif.com


### Предисловие. 1:05

На этом занятии мы:
- Познакомимся с базовыми понятиями в контексте применения Docker.
- Узнаем состав и назначение компонентов экосистемы Docker.
- Рассмотрим базовую архитектуру Docker.
- Рассмотрим пример жизненного цикла Docker-контейнера.
- Научимся упаковывать приложения в Docker!
- А также научимся готовый докер -образ сохранять во внешнем докер-реджистре


### План занятия
```yml
1. Введение в Docker
2. Экосистема Docker
3. Архитектура Docker
4. Жизненный цикл Docker-контейнера
5. Собираем первый Docker-контейнер
6. Итоги
7. Домашнее задание
```
### Введение в Docker
#### Контейнер. 2:05
Предшественник Докера - LXC контейнер.
Докер - это его следующая реинкарнация.
Самая важная вещь - это то, что мы можем декларативно описывать конфигурацию собираемого контейнера.

**Контейнер** — это способ упаковать приложение и все его зависимости в единый образ. 
Этот образ запускается в изолированной среде, не влияющей на основную операционную систему.
Используется ядро все той же хост-машины, на которой работает движок докера. Но при этом внутрянка контейнера находится в абсолютно изолированной среде. Используется ядро Linux NameSpaces для изоляции и модуль ядра Linux SeeGroops для разграниечения прав исполняемого RunTime самого контейнера.

Контейнеры позволяют отделить приложение от инфраструктуры: разработчики просто создают приложение, 
упаковывают все зависимости и настройки в единый образ. 
Затем этот образ можно запускать на других системах, не беспокоясь, что приложение не запустится.

Запускать на других чичтемах можно благодаря тому, что мы можем собранный образ отправить в удаленный реестр образов, затем командой ` docker pull ` выкачать образ на любой хост и запустить.

#### Docker. 4:55
Docker — это платформа для разработки, доставки и запуска контейнерных приложений.
- Docker позволяет:
  - создавать контейнеры,
  - автоматизировать их запуск и развертывание,
  - управлять жизненным циклом,
  - запускать множество контейнеров на одной хост-машине.

Контейнеризация похожа на виртуализацию, но это не одно и то же.
- 5:38. Контейнеры - это более изощренный вид изоляции за счет того, что для контейнеров используется упрощенная виртуализация на основе 3 вида виртуализации (Docker работает на виртуалзации уровня ОС)

#### Docker. 6:28
Виртуализация работает как отдельный компьютер со своим виртуальным оборудованием и операционной системой. 
При этом внутри одной ОС можно запустить другую ОС.

В случае контейнеризации, виртуальная среда запускается прямо из ядра основной операционной системы и не виртуализирует оборудование.
Важный момент №1. Мы монтируем внутрь контейнера физические устройства, доступные на хостовой машине.
Мы используем ядро хостовой системы для выполнения RunTime внутри докер-контейнера и не виртуализируем оборудование. Оно монтируется внутрь контейнера.
- 7:40. Возможно даже подключение к контейнеру отдельной физической сетевой карты с отдельным мак-адресов. Лектор обещал рассказать как это сделать.
При этом, так как контейнеры не виртуализируют оборудование, они потребляют намного меньше ресурсов.

#### Преимущества использования Docker. 08:11
- Контейнеры в целом упрощают работу как программистам, так и инженерам, которые развертывают эти приложения.
- **Docker решает проблемы зависимостей и рабочего окружения.** 
  - 08:35 Подробности
  - 10:05 О зависимостях. При создании ВМ мы стараемся создать ее из какого-то ране собранного образа. Это значит, что мы клонируем внутрь ВМ все ПО, которое содержится внутри исходног образа.
  - 10:45 В случае с контейнерами мы вольны выбирать исходный образ (то дистрибутив который нам больше подходит, например легче и меньше). Например      DebianSlim, Ubuntu Slim, Alpine Linux, в котором вообще ничего нет. И таким образом у нас появляется абсолютно чистый контейнер, в котором нет ничего лишнего и мы ставим туда только необходимые системные зависимости для того, чтобы реализовать ту задачу, которая нам нужна.
  - 11:20 Если вы когда-нибуть пробовали развернуть ОС Alpine в Докере и погружались внутрь контейнера, то видели, что там нет вообще ничего из системных утилит. Нет ни телнет, ни нет-стат утилит. Это сделано для экономии места и чтобы минимально ужать исходный образ и дать только необходимую структуру файловой системы для того, чтобы все работало. Далее мы вольны в этот образ доустановить все что нам нужно для запуска нашего приложения - бибилиотеки, системные утилиты, конфигурационные файлы. Все это можно добавить и установить во время сборки.
- Контейнеры позволяют упаковать в единый образ приложение и все его зависимости: библиотеки, системные утилиты 
и файлы конфигурации.

#### Преимущества использования Docker. 12:33
**Docker упрощает перенос приложения на другую инфраструктуру.**

Например, разработчики создают приложение в системе, там все настроено и приложение работает. 
Когда приложение готово, его нужно перенести в систему тестирования и затем в продуктивную среду. 
И если в этих системах будет не хватать какой-нибудь зависимости, то приложение не будет работать. 
В этом случае программистам придется отвлечься от разработки и совместно с командой поддержки разбираться в ситуации.
Контейнеры позволяют избежать такой проблемы, потому что они содержат в себе все необходимое для запуска приложения.
- Контейнеры позволяют ыполнить переезд с одной физической инфраструктуры еа другую.

#### Изоляция и безопасность Docker. 18:19
**Контейнер Docker** — это набор процессов, изолированных от основной операционной системы.
Приложения работают только внутри контейнеров, и не имеют доступа к основной операционной системе.
Это повышает безопасность приложений, потому что они не смогут случайно или умышленно навредить основной системе.

Если приложение в контейнере завершится с ошибкой или зависнет, это никак не затронет основную ОС.

### Экосистема Docker. 20:37
#### Компоненты экосистемы Docker

1. **Docker Daemon** (Docker демон) — сервер контейнеров, входящий в состав программных средств Docker. 
Демон управляет Docker-объектами (сети, хранилища, образы и контейнеры). 
Демон также может связываться с другими демонами для управления сервисами Docker.

1. **Docker Client / CLI** (Docker клиент) — интерфейс взаимодействия пользователя с Docker-демоном. 
Клиент и Демон — важнейшие компоненты «движка» Докера (Docker Engine). 
Клиент Docker может взаимодействовать с несколькими демонами.
22:30 - в случае с Docker Swarm Докер-клиент может общаться в разными докер-демонами, если у того удаленного хоста докер-демон доступен по сети.

1. 22:58 **Docker Image** (Docker образ) — файл, включающий зависимости, сведения, конфигурацию для дальнейшего
развертывания и инициализации контейнера.
- 23:15 Далее мы рассмотрим Докер образ, внутри которого будет собираться Ansible со всеми зависимостями

1. **Dockerﬁle** (Docker файл) — описание правил (манифест) сборки образа, в котором первая строка указывает на базовый образ.
Последующие команды выполняют копирование файлов и установку программ для создания определенной среды разработки со
своим набором переменных окружения и прочих параметров.
- 23:40 В докер-файле (манифесте) первая строка ссылается на Docker-Image, с которого начинается сборка, а последующие команды выполняют копирование файлов, установку ПО для создания определенной среды для выполнения RunTime самого приложения, ради которого этот образ и собирался

1. 24:08 **Docker Container** (Docker контейнер) — это легкий, автономный исполняемый пакет программного обеспечения, который запускается на базе ранее собранного образа и который включает в себя все необходимое для запуска приложения: код, среду выполнения, системные инструменты, системные библиотеки и настройки.
- 24:26 По сути контейнер - это запущенный Docker-Image (ранее собранный), полученный посредством сборки на основе описанного манифеста (докер-файла)
- 38:50 Докер-демон из образа ОС делает контейнер

1. 24:40 **Volume** (Том хранения данных) — эмуляция файловой системы для осуществления операций чтения и записи. 
Она создается автоматически с контейнером, поскольку некоторые приложения осуществляют персистентное хранение данных.
Для самого контейнера Волюм - это эмуляция файловой системы для выполнения ввода-вывода информации на хост-систему. Волюмы сосздаются автоматически, если это указано в конфигурации самого контейнера.
Есть состояния контейнеров Стайтлесс (без состояния, которые не используют никаких персистентных данных внутри себя) и стейтфулл (как раз те контейнеры, которые обращаются к томам хранения данных для сохранения тех данных, которые нельзя потерять при удалении самого контейнера). 

1. 27:12 **Docker Registry** (Реестр Docker контейнеров) — зарезервированный сервер, используемый для хранения docker-образов.
- Это выделенный сервер, на котором происходит хранение собранных контейнеров

1. **Docker Trusted Registry** (Доверенный реестр Docker или DTR) — служба docker-реестра для инсталляции на локальном компьютере или сети компании.

1. **Docker Hub** (Docker Хаб) — общедоступный и бесплатный репозиторий, предназначенный для хранения образов с различным программным обеспечением. Доступен по https://hub.docker.com

1. 29:15 **Docker Host** (Docker хост) — среда, на которой запускается Docker Engine (Docker Demon) в виде системного демона для запуска
контейнеров с программным обеспечением, указанным в Docker файле.

1. 30:05 **Docker Networks** (Docker сети) — применяются для организации сетевого взаимодействия между приложениями,
развернутыми в контейнерах.
#### Dicker сети. 30:45
На уровне файловой системы сеть в Docker - это json конфгурация.
Существует несколько режимов работы Docker сети.
Например: 
- bridge,
- host, 
- overlay, 
- macvlan и 
- none.
##### Типы режимов работы сети в Docker
1. **Bridge** (Мост) — сетевой драйвер по умолчанию. Если вы не укажете драйвер, этот тип сети, инициализируется
автоматически. Мостовые сети обычно используются, когда ваши приложения работают в автономных контейнерах,
которым необходимо обмениваться данными.

1. **Host** (Хост) — применяется для автономных контейнеров, этот тип сети удаляет слой изоляции между контейнером и Docker
хостом и напрямую использует сеть хоста.

1. 33:13 **Overlay** (Оверлей) — оверлейные сети соединяют вместе несколько демонов Docker и позволяют службам Docker Swarm взаимодействовать друг с другом в режиме кластера.
Это **общий случай логической сети**, создаваемой поверх другой сети. 
Узлы оверлейной сети могут быть связаны либо физическим соединением, либо логическим, для которого в
основной сети существуют один или несколько соответствующих маршрутов из физических соединений. 
Эта **стратегия устраняет необходимость выполнять маршрутизацию на уровне ОС** между этими контейнерами.

1. 34:50 **Macvlan** — сети Macvlan позволяют назначать MAC-адрес контейнеру, чтобы он отображался как физическое 
устройство в вашей сети. Демон Docker направляет трафик в контейнеры по их MAC-адресам. 

Использование драйвера macvlan иногда является лучшим выбором при работе с устаревшими
приложениями, которые ожидают прямого подключения к физической сети, а не маршрутизации через 
сетевой стек Docker хоста .

Можно эмулровать сетевые устрйства с помощью контейнеров и присвоеня м мак-адресов.

1. **None** — в этом режиме работы отключаются все сети. 
Такой режим работы сети обычно используется вместе с сторонними сетевыми драйверами.
None недоступен для служб Docker Swarm. 

Вы можете установить и использовать сторонние сетевые плагины с Docker. 
Эти плагины доступны в Docker Hub или у сторонних поставщиков. Пример плагина: weave2.
https://www.weave.works/docs/net/latest/install/plugin/plugin-v2/

### Архитектура Docker. 38:10
![Архитектура Docker](/05-virt-03-docker/img/architectura-docker.png)
Подробнее https://docs.docker.com/get-started/overview

### 39:40 Жизненный цикл Docker-контейнера в командах Docker CLI (Command Line Interface)
#### 1. Загрузка образа из Docker реестра на Docker хост. 39:40 

Команда ` docker pull `
```bash
# Пример загрузки образа Docker контейнера "hello-world" из публичного репозитория hub.docker.com

$ docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:61bd3cb6014296e214ff4c6407a5a7e7092dfa8eefdbbec539e133e97f63e09f
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest

$ docker image ls
REPOSITORY    TAG   IMAGE ID    CREATED       SIZE
hello-world latest d1165f221234 6 months ago  13.3kB
```

#### 2. Запуск Docker контейнера из локального реестра на Docker хосте. 41:57
Команда ` docker run ` 
```bash
# Пример запуска образа Docker контейнера "hello-world"

$ docker run hello-world
Hello from Docker!
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
(amd64)
3. The Docker daemon created a new container from that image which runs the
executable that produces the output you are currently reading.
4. The Docker daemon streamed that output to the Docker client, which sent it
to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
$ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
https://hub.docker.com/
For more examples and ideas, visit:
https://docs.docker.com/get-started/
```

#### 3. Запуск образа в интерактивном режиме из публичного репозитория hub.docker.com 43:58
Команда ` docker run -it ` [в интерактивном режиме] позволяет также войт внутрь контейнера.

```bash
# Запуск в интерактивном режиме образа "ubuntu" из публичного репозитория hub.docker.com
-i - интераквный режм
-t - спользовать терминал

$ docker run -it ubuntu bash # bash - какую оболочку мы хотим получить после входа
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
35807b77a593: Pull complete
Digest: sha256:9d6a8699fb5c9c39cf08a0871bd6219f0400981c570894cd8cbea30d3424a31f
Status: Downloaded newer image for ubuntu:latest

#Вошли внутрь контейнера в оболочку bash. Смотрим версю ОС.
$ root@b65a0676dd1d:/# cat /etc/*release
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
root@b65a0676dd1d:/# exit
```
- ID контейнера  ID образа всегда разные, а ID контейнера всегда ункальные для каждого запуска. Это сделано для того чтобы можно было запускать много однаковых контейнеров нв одном хосте
#### 4. Запуск какой-либо команды в запущенном Docker контейнере. 45:35
Команда ` docker exec `
```bash
# Запуск контейнеа в фоновом режиме -d (detach, отстегнуть)
$ docker run -d nginx
ba2a5dfd1b05dc380765c877722ac56932376abad4d8bb85927ae35bf101bf98

#Смотрим состояне контейнера. Видим, что он запущен
$ docker ps
CONTAINER ID    IMAGE  COMMAND                CREATED       STATUS        PORTS   NAMES
ba2a5dfd1b05    nginx  "/docker-entrypoint.…" 4 seconds ago Up 3 seconds  80/tcp  objective_yalow

# Запуск команды "nginx -v" в запущенном контейнере
$ docker exec -it objective_yalow nginx -v
nginx version: nginx/1.21.3
```
#### 5. Остановка запущенного Docker контейнера. 48:02
Команда ` docker stop `
```bash
# Остановка запущенного Docker контейнера с именем "objective_yalow".
$ docker stop objective_yalow #Можно указывать ID контейнера

#Смотрим состояне контейнера. Видим, что запущенных контейнеров нет
$ docker ps

$ docker ps -a
```
#### 6. Удаление остановленного Docker контейнера. 49:37
Команда ` docker rm `. После остановки контейнер не удаляется. 
```bash
# Удаление остановленного Docker контейнера.
$ docker rm objective_yalow
objective_yalow

$ docker ps

$ docker ps -a
```
#### 7. Удаление образа Docker контейнера. 50:25
Команда ` docker rmi ` для удаления ранее собранного образа (i - images).
```bash
# Удаление образа Docker контейнера.
$ docker rmi nginx
Untagged: nginx:latest
Untagged: nginx@sha256:853b221d3341add7aaadf5f81dd088ea943ab9c918766e295321294b035f3f3e
Deleted: sha256:ad4c705f24d392b982b2f0747704b1c5162e45674294d5640cca7076eba2865d
Deleted: sha256:cf45bd1acd3159a35178bfe8a63f910f010990175050ea6c8c333ba3afaf5123
Deleted: sha256:a9e7419d7f7c4fe55c85ce08c4f0a8b45abe9b714aa19880f553859797e0332c
Deleted: sha256:13184aa93ccd585fade03704e048828c29eed86090e7399b208edbe022aaf563
Deleted: sha256:3161f310d154031dbd57f90c07715335a25a31bcf20a4abf3e040ab86bcac633
Deleted: sha256:88f95677408c5f02b15064ad1f41a2c74e40e1800cd3536f8fb45b9e6939704b
Deleted: sha256:d000633a56813933cb0ac5ee3246cf7a4c0205db6290018a169d7cb096581046

$ docker images
REPOSITORY    TAG
```

#### 8. Удаление неиспользуемых Docker образов. 50:21
Команда ` docker system prune `
```bash
# Удаление неиспользуемых Docker образов.
$ docker system prune
WARNING! This will remove:
- all stopped containers
- all networks not used by at least one container
- all dangling images
- all dangling build cache
Are you sure you want to continue? [y/N] y
Deleted Containers:
b65a0676dd1d65025c4954d7b20bca108464d3e347225bf3728fcba896e5dbc3
c1fda7c70de824e08c98059ab861e73e8d3138c95632c2c939cfc3006168d281
c0522f9fd4e146844b425246418bf2814072d457aafd151d7f9f3d76d5750412
d824b31993e9f31770a5acbd90061ba435e5eca5b42ce8e216ea5754dbd54e56
c052919f6d049ad559a2d2faac5309f1aa28ac932b8cdfc3258fa532f8bf9fd1
Total reclaimed space: 40B

$ docker image ls
```
#### 9. Удаление всех Docker образов. 53:23
Команда ` ocker system prune -a -f ` (ключ -a использовать с осторожностью!)
```bash
# Удаление всех Docker образов, контейнеров, сетей и конфгурацй. Возвращение к первоначальному состояню.

$ docker system prune -a -f
Deleted Images:
untagged: hello-world:latest
untagged: hello-world@sha256:61bd3cb6014296e214ff4c6407a5a7e7092dfa8eefdbbec539e133e97f63e09f
deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
untagged: ubuntu:latest
untagged: ubuntu@sha256:9d6a8699fb5c9c39cf08a0871bd6219f0400981c570894cd8cbea30d3424a31f
deleted: sha256:fb52e22af1b01869e23e75089c368a1130fa538946d0411d47f964f8b1076180
deleted: sha256:4942a1abcbfa1c325b1d7ed93d3cf6020f555be706672308a4a4a6b6d631d2e7
Total reclaimed space: 72.79MB

$ docker image ls
```

#### Сравнение команд ` Docker exec ` и` Docker Run ` 55:23

docker exec — yourContainerName bash
docker run — yourImageName bash

Ключевые различия:
- docker exec — предназначен для выполнения бинарного файла, отличного от указанного в ENTRYPOINT (если он существует в манифесте образа) в работающем контейнере.
- docker run — предварительно скачивает образ (если образ не обнаружен в локальном реестре) и запускает контейнер из образа. Без дополнительных параметров запускается бинарный файл, указанный в качестве точки входа для выполнения.

#### Вывод диагностической информации из запущенного Docker контейнера. 56:38
Команда ` docker logs ` — если хотите получить диагностическую информацию из запущенного контейнера.
```bash
# Диагностика Docker контейнера.

$ docker logs --tail 1 stoic_archimedes
2021/09/19 15:04:15 [notice] 1#1: start worker process 32

$ docker logs -f stoic_archimedes
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2021/09/19 15:04:15 [notice] 1#1: using the "epoll" event method
2021/09/19 15:04:15 [notice] 1#1: nginx/1.21.3
2021/09/19 15:04:15 [notice] 1#1: built by gcc 8.3.0 (Debian 8.3.0-6)
2021/09/19 15:04:15 [notice] 1#1: OS: Linux 5.10.25-linuxkit
2021/09/19 15:04:15 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2021/09/19 15:04:15 [notice] 1#1: start worker processes
2021/09/19 15:04:15 [notice] 1#1: start worker process 31
2021/09/19 15:04:15 [notice] 1#1: start worker process 32
```
#### Вывод диагностической информации Docker контейнера. 57:33
Команда ` docker attach ` — если необходимо перенаправить поток данных в контейнер. Это ручная работа и это угроза автоматзации. Необходимо для эксперментов, дебагов и т.д.
```bash

#Запуск контейнера "nginx" в фоновом режме
$ docker run -d nginx
1cff1abd6615d651a5d01a09431ec6a78e040eec6a33b0621a663f7f4fc23584

#Смотрим состояние контейнера
$ docker ps

# Перенаправление потока в Docker контейнер.
$ docker attach hopeful_meitner
^C2021/09/19 15:09:52 [notice] 1#1: signal 2 (SIGINT) received, exiting
2021/09/19 15:09:52 [notice] 33#33: exiting
2021/09/19 15:09:52 [notice] 32#32: exiting
2021/09/19 15:09:52 [notice] 33#33: exit
2021/09/19 15:09:52 [notice] 32#32: exit
2021/09/19 15:09:52 [notice] 1#1: signal 17 (SIGCHLD) received from 32
2021/09/19 15:09:52 [notice] 1#1: worker process 32 exited with code 0
2021/09/19 15:09:52 [notice] 1#1: signal 17 (SIGCHLD) received from 33
2021/09/19 15:09:52 [notice] 1#1: worker process 33 exited with code 0
2021/09/19 15:09:52 [notice] 1#1: exit

$ docker ps
CONTAINER ID  IMAGE COMMAND CREATED STATUS  PORTS NAMES
```

#### Сходство с ООП. 58:25
Сходство с объектно-ориентированным программированием:
- Образы концептуально подобны **классам**.
- Слои концептуально похожи на **наследование**.
- Контейнеры концептуально похожи на **экземпляры классов**.

#### Для чего и где использовать теги образов? 1:01:19
- Теги Docker образов схожи с Git-тегами. Они представляют собой указатель на образ с соответствующим идентификатором.
- Добавление тега не переименовывает образ, а исключительно добавляет тег.

Пример: при использовании собственного реестра **docker.mycompany.com/jenkins/jenkins-ant:1.10.5**
- где:
  - docker.mycompany.com/jenkins/jenkins-ant — это изначальное имя образа, а 
  - 1.10.5 — версия. 

Чтобы выполнить docker pull с указанием тега, нужно указать так:

```bash
# Загрузка Docker образа из частного реестра.
$ docker pull docker.mycompany.com/jenkins/jenkins-ant:1.10.5
```

Образы могут обладать тегами для определения версий или вариантов образа.
- **docker pull ubuntu** будет ссылаться на **ubuntu:latest**.
- Тег **latest** часто является самым последним состоянием (зачастую не стабильным).
- **ubuntu** — это по сути: **library/ubuntu** или index.docker.io/library/ubuntu

- 1:01:44 Необходимо использовать теги:
  - при использовании образа в продакшн окружении.
  - чтобы гарантировать, что одна и та же версия будет использоваться везде (на всех окружениях).
  - чтобы получить идемпотентный результат.

Не стоит использовать теги:
- при проведении экспресс-тестирования и прототипирования.
- при проведении экспериментов.
- когда вам нужна последняя версия.

#### Как корректно применять тег latest? 1:03:09
- Убедитесь, что вы задали тег в целом и этот тег корректный. **Если тег не задан, то по умолчанию будет использован тег “latest”.**
- Проблема с тегом “latest” — никто не знает, на что он указывает:
  - последнее изменение в репозитории?
  - последний коммит в какой-то ветке? и какой именно?
  - последний созданный git тег в данном репозитории ?
  - какая-то произвольная версия?
- Если вы каждый раз перезаписываете “latest”, то теряете возможность отката на предыдущую версию.
- Теги образов должны иметь осмысленные имена, то есть соответствовать ветвям кода, тегам или хэшам.

Никогда не использовать в продакшене контейнеры с тегом latest

#### Контекст сборки в Docker 1:04:20
- **Контекст сборки** — это рабочая директория, содержащая Dockerﬁle и дополнительные файлы (части сборки). Зачастую, это текущая директория “ . ”, передается в команде при сборке docker образа.
- Содержание контекста сборки отправляется (в виде архива) **Docker-клиентом демону Docker.**
- Чем больше дискового пространства занимает директория контекста сборки, тем потенциально дольше займет сборка образа.


#### Переименование запущенных контейнеров 1:05:25
Вы можете переименовать контейнеры с помощью команды ` docker rename `.
Это позволяет "освободить" имя, не удаляя текущий (работающий) Docker контейнер.
```bash
# Запускаем Docker контейнер.
$ docker run -d nginx
f49eb0b8ddac59bc7b34421a86371f788cca733056f08e11bf2a1bac0ad0fe9b

#Контейнер запущен
$ docker ps
CONTAINER ID    IMAGE   COMMAND
f49eb0b8ddac    nginx   "/docker-entrypoint.…"

# Переименование запущенного Docker контейнера.
$ docker rename eloquent_cannon nginx_netology
18:46:16 @ ~ []
└─ $ ▶ docker ps
NAMES
eloquent_cannon
NAMES
nginx_netology
```

#### Volume. Подключение локальной директории из хостовой машины в контейнер для сохранения и общего использования данных. 1:06:17
Команда ` docker run -v ` 
Можно реализовать:
- Постоянное хранение данных, полученных в результате запущенного в контейнере приложения.
- Совместное использование данных в двух и более запущенных контейнерах.
```bash
# Подключение локальной директории для использования в Docker контейнере.
$ docker run -v /local-data:/data-in-container --name container_name -d image-name
# Пояснение команды
# -v - ключ команды
# /local-data - указываем локальную директорию
# : - символ двоеточия
# /data-in-container - директория внутри контейнера
# --name - ключ команды 
# container_name - имя контейнера
# -d - ключ команды для запуска контейнера в фоновом режиме
# image-name - имя образа
#
```
- Есть два вида Volume
  - 1:06:48 обычное монтирование локальных директорий внутрь контейнера (в какую-то существующую директорию)
  - 1:07:00 когда мы гороврим  ` dockervolume create `  мы создаем некий объект внутри Докер-демона в виде виртуальной директории. На самом деле эта директория находится в ` /var/lib/docker/bla-bla-bla ` на оверлейном сторадже, который использует Докер. И внутрь этого контейнера уже монитруется виртуальная дирктория, но эта виртуальная директория все также находится у нас на хост-машине. Разница в том, что управляет ли логикой внешней директории сам Докер-демон, либо управляет просто пользователь ОС Докер-хоста.

#### Создание и использование сети для запущенных контейнеров. 1:09:28
Для реализации сетевого соединения между контейнерами:
- Создайте новую виртуальную сеть или используйте существующую.
- Запустите новый контейнер из образа и запустте сеть
- Подключите сеть к уже запущенному контейнеру.

Чтобы не делать это вручную лучше использовать Dicker Compose

Возможно подключение контейнера(ов) к одной или более сетей.
```bash
# Создане новой виртуальной сети
$ docker network create network-name

# Запуск контейнера из образа, запуск сети
$ docker run -d --name=container-name --net=network-name image-name

#Подключене контейнера к сети
$ docker network connect network-name container-name
```

### Собираем первый Docker-контейнер 1:10:50
#### Dockerﬁle. 1:10:54.
Манифест **Docker** образа в котором **будет выполнятся Ansible**.
```bash
# Манифест Docker образа.

FROM alpine:3.14

RUN CARGO_NET_GIT_FETCH_WITH_CLI=1 && \
    apk --no-cache add \
    sudo python3 py3-pip openssl ca-certificates sshpass openssh-client rsync git && \
    apk --no-cache add
    --virtual build-dependencies python3-dev libffi-dev musl-dev gcc cargo openssl-dev \
    libressl-dev \
    build-base && \
    pip install --upgrade pip wheel && \
    pip install --upgrade cryptography cffi && \
    pip install ansible==2.9.24 && \2
    pip install mitogen ansible-lint jmespath && \
    pip install --upgrade pywinrm && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/* && \    
    rm -rf /root/.cache/pip && \
    rm -rf /root/.cargo

RUN mkdir /ansible && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts

WORKDIR /ansible

CMD [ "ansible-playbook", "--version" ]
```

#### Собираем Docker образ. 1 час 12 минут 33 секунд
Собираем Docker образ, в котором будет выполнятся Ansible.
```bash
# Переходим в директорию, где лежит Dockerfile
$ cd /Users/olegbukatchuk/git/netology.ru/virt-homeworks/05-virt-03-docker-usage/src/build/ansible

#Запускаем сборку с тегом (ключ -t). Тег называется "olegbukatchuk/ansible:2.9.24". 
#И указать контекст сборки ту самую директорю (точку ` . `) в которой мы находимся.
$ docker build -t olegbukatchuk/ansible:2.9.24 .
... more output strings)))
OK: 98 MiB in 69 packages
Step 3/5 : RUN mkdir /ansible &&
mkdir -p /etc/ansible &&
/etc/ansible/hosts
---> Running in 05d83f4f0b02
Removing intermediate container 05d83f4f0b02
---> d6bbad65c025
Step 4/5 : WORKDIR /ansible
---> Running in 2d744a795644
Removing intermediate container 2d744a795644
---> 6788cf704b9c
Step 5/5 : CMD [ "ansible-playbook", "--version" ]
---> Running in 81d1f8ad28af
Removing intermediate container 81d1f8ad28af
---> b5878eb55f00
Successfully built b5878eb55f00  #Сборка завершена
Successfully tagged olegbukatchuk/ansible:2.9.24  #Добавлен тег "olegbukatchuk/ansible:2.9.24"
echo 'localhost' >

# !!! Lifehack: verbose mode !!!
$ DOCKER_BUILDKIT=0 docker build -t olegbukatchuk/ansible:2.9.24 .
```

#### Загрузка в публичный реестр. Выгружаем Docker образ в публичный реестр
Команда ` docker push `
```bash
# Авторизация в публичном реестре Docker Hub.
$ docker login -u olegbukatchuk
Password:
Login Succeeded
```

#### Выгружаем Docker образ в публичный ![реестр](http://hub.docker.com)
Перед этм создать на Docker Hub дректорю для сохраненя образов. В прмере это директория /ansile
Команда ` docker push `
```bash
$ docker push olegbukatchuk/ansible:2.9.24
The push refers to repository [docker.io/olegbukatchuk/ansible]
444dd64430d4: Pushed
fb7eb8195ff4: Pushed
e2eb06d8af82: Mounted from library/alpine
2.9.24: digest: sha256:01460d9c51dddfe785859c5968e1b33a467a5d5a6d0176dbc2e5b73f5c98fc8e size:
947
```
Теперь этот Docker образ находится в публичном реестре и доступен для использования всем по ![адресу](https://hub.docker.com/repository/docker/olegbukatchuk/ansible).
```bash
# Загрузка из публичного реестра Docker Hub.
$ docker pull olegbukatchuk/ansible:2.9.24
```
### Итоги
#### Что мы узнали?

- Рассмотрели, компоненты экосистемы Docker;
- Узнали о преимуществах, использования контейнеров;
- Рассмотрели базовый набор Docker CLI для управления жизненным циклом контейнеров;
- Научились загружать, собирать, запускать, переименовывать, удалять контейнеры, а также очищать локальный реестр от ненужных Docker образов;
- Поняли, как можно использовать Docker в контексте 
  - Continuous integration, 
  - Continuous delivery
  - Continuous deployment.

### Домашнее задание
Давайте посмотрим ваше домашнее задание.
- Вопросы по домашней работе задавайте в чате мессенджера Slack.
- Задачи можно сдавать по частям.
- Зачёт по домашней работе проставляется после того, как приняты все задачи.

### Задавайте вопросы ипишите отзыв о лекции!
Олег Букатчук
olegbukatchuk

```ps
<pre>root@PC-Ubuntu:/usr/bin# 
root@PC-Ubuntu:/usr/bin# 
root@PC-Ubuntu:/usr/bin# sudo sh -c &quot;echo &apos;deb http://dl.google.com/linux/chrome/deb/ stable main&apos; &gt;&gt; /etc/apt/sources.list.d/google.list&quot;
root@PC-Ubuntu:/usr/bin# 
root@PC-Ubuntu:/usr/bin# apt-get update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Пол:2 http://dl.google.com/linux/chrome/deb stable InRelease [1 811 B]                                                                                                       
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease                                                                                                                                            
Сущ:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                                                                                                                                          
Сущ:5 http://security.ubuntu.com/ubuntu focal-security InRelease                                                                                                                                             
Сущ:6 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Сущ:7 https://apt.releases.hashicorp.com focal InRelease                                                                                                                     
Сущ:8 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                             
Пол:9 http://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1 090 B]
Получено 2 901 B за 2с (1 555 B/s)      
Чтение списков пакетов… Готово
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «http://dl.google.com/linux/chrome/deb stable InRelease» не поддерживает архитектуру «i386»
root@PC-Ubuntu:/usr/bin# 
root@PC-Ubuntu:/usr/bin# apt-get install google-chrome-stable
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие НОВЫЕ пакеты будут установлены:
  google-chrome-stable
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 7 пакетов не обновлено.
Необходимо скачать 90,8 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 289 MB.
Пол:1 http://dl.google.com/linux/chrome/deb stable/main amd64 google-chrome-stable amd64 96.0.4664.45-1 [90,8 MB]
Получено 90,8 MB за 42с (2 142 kB/s)                                                                                                                                                                         
Выбор ранее не выбранного пакета google-chrome-stable.
(Чтение базы данных … на данный момент установлено 217806 файлов и каталогов.)
Подготовка к распаковке …/google-chrome-stable_96.0.4664.45-1_amd64.deb …
Распаковывается google-chrome-stable (96.0.4664.45-1) …
Настраивается пакет google-chrome-stable (96.0.4664.45-1) …
update-alternatives: используется /usr/bin/google-chrome-stable для предоставления /usr/bin/x-www-browser (x-www-browser) в автоматическом режиме
update-alternatives: используется /usr/bin/google-chrome-stable для предоставления /usr/bin/gnome-www-browser (gnome-www-browser) в автоматическом режиме
update-alternatives: используется /usr/bin/google-chrome-stable для предоставления /usr/bin/google-chrome (google-chrome) в автоматическом режиме
Обрабатываются триггеры для mime-support (3.64ubuntu1) …
Обрабатываются триггеры для gnome-menus (3.36.0-1ubuntu1) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для desktop-file-utils (0.24-1ubuntu3) …
root@PC-Ubuntu:/usr/bin# 
root@PC-Ubuntu:/usr/bin# 
</pre>
```
