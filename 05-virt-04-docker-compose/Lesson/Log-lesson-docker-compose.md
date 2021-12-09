## Логи выполнения домашнего задания на физической ОС Ubuntu на Sergey-PC
### Создаем директории для учебного проекта Docker-Compose, устанавливаем Git, копируем директорию "src" из клонированного репозитория с домашним заданием
```bash
maestro@PC-Ubuntu:~/Рабочий стол$ sudo -i
[sudo] пароль для maestro: 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# type git
-bash: type: git: не найден
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# apt install git
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  git-man liberror-perl
Предлагаемые пакеты:
  git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk
  gitweb git-cvs git-mediawiki git-svn
Следующие НОВЫЕ пакеты будут установлены:
  git git-man liberror-perl
Обновлено 0 пакетов, установлено 3 новых пакетов, для удаления отмечено 0 пакетов, и 11 пакетов не обновлено.
Необходимо скачать 5 465 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 38,4 MB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 liberror-perl all 0.17029-1 [26,5 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 git-man all 1:2.25.1-1ubuntu3.2 [884 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 git amd64 1:2.25.1-1ubuntu3.2 [4 554 kB]
Получено 5 465 kB за 3с (2 030 kB/s)       
Выбор ранее не выбранного пакета liberror-perl.
(Чтение базы данных … на данный момент установлен 217941 файл и каталог.)
Подготовка к распаковке …/liberror-perl_0.17029-1_all.deb …
Распаковывается liberror-perl (0.17029-1) …
Выбор ранее не выбранного пакета git-man.
Подготовка к распаковке …/git-man_1%3a2.25.1-1ubuntu3.2_all.deb …
Распаковывается git-man (1:2.25.1-1ubuntu3.2) …
Выбор ранее не выбранного пакета git.
Подготовка к распаковке …/git_1%3a2.25.1-1ubuntu3.2_amd64.deb …
Распаковывается git (1:2.25.1-1ubuntu3.2) …
Настраивается пакет liberror-perl (0.17029-1) …
Настраивается пакет git-man (1:2.25.1-1ubuntu3.2) …
Настраивается пакет git (1:2.25.1-1ubuntu3.2) …
Обрабатываются триггеры для man-db (2.9.1-1) …
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# type git
git является /usr/bin/git
```
#### Создаем директорию проекта
```bash
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# ls -l
итого 12
drwxr-xr-x 3 root root 4096 дек  5 13:14  snap
drwxr-xr-x 4 root root 4096 дек  5 15:48  vagrant-project
drwx------ 5 root root 4096 дек  5 18:20 'VirtualBox VMs'
root@PC-Ubuntu:~# mkdir -p netology-project
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cd netology-project/
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# ls -l
итого 0
root@PC-Ubuntu:~/netology-project# mkdir -p Docker-Compose
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# cd Docker-Compose/
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# git status
fatal: не найден git репозиторий (или один из родительских каталогов): .git
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
```
#### Инициализируем Git
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose# git init
Инициализирован пустой репозиторий Git в /root/netology-project/Docker-Compose/.git/
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# git config --list --show-origin 
file:.git/config        core.repositoryformatversion=0
file:.git/config        core.filemode=true
file:.git/config        core.bare=false
file:.git/config        core.logallrefupdates=true
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# git config --global user.name "Sergey Zakharov"
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# git config --global user.email zakharovnpa@gmail.com 
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# cd ..
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# mkdir -p 02-virt-admin
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# cd 02-virt-admin/
root@PC-Ubuntu:~/netology-project/02-virt-admin# 
root@PC-Ubuntu:~/netology-project/02-virt-admin# git init
Инициализирован пустой репозиторий Git в /root/netology-project/02-virt-admin/.git/
root@PC-Ubuntu:~/netology-project/02-virt-admin# 
root@PC-Ubuntu:~/netology-project/02-virt-admin# cd ..
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# git clone https://github.com/zakharovnpa/02-virt-admin-homeworks.git 02-virt-admin
fatal: целевой путь «02-virt-admin» уже существует и не является пустым каталогом.
root@PC-Ubuntu:~/netology-project# 
```
#### Клонируем репозиторий с заданием
```bash
root@PC-Ubuntu:~/netology-project# git clone https://github.com/zakharovnpa/02-virt-admin-homeworks.git 2-virt-admin
Клонирование в «2-virt-admin»…
remote: Enumerating objects: 957, done.
remote: Counting objects: 100% (957/957), done.
remote: Compressing objects: 100% (870/870), done.
remote: Total 957 (delta 514), reused 11 (delta 2), pack-reused 0
Получение объектов: 100% (957/957), 1.73 МиБ | 1.41 МиБ/с, готово.
Определение изменений: 100% (514/514), готово.
```
#### Копируем директорию "src" из репозитория с заданием в папку проекта "Docker-Compose"
```bash
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# ls -l
итого 12
drwxr-xr-x  3 root root 4096 дек  9 15:48 02-virt-admin
drwxr-xr-x 11 root root 4096 дек  9 15:51 2-virt-admin
drwxr-xr-x  3 root root 4096 дек  9 15:28 Docker-Compose
root@PC-Ubuntu:~/netology-project# 
root@PC-Ubuntu:~/netology-project# cd 2-virt-admin/
root@PC-Ubuntu:~/netology-project/2-virt-admin# 
root@PC-Ubuntu:~/netology-project/2-virt-admin# ls -l
итого 36
drwxr-xr-x 2 root root 4096 дек  9 15:51 05-virt-01-basics
drwxr-xr-x 5 root root 4096 дек  9 15:51 05-virt-02-iaac
drwxr-xr-x 5 root root 4096 дек  9 15:51 05-virt-03-docker
drwxr-xr-x 5 root root 4096 дек  9 15:51 05-virt-04-docker-compose
drwxr-xr-x 2 root root 4096 дек  9 15:51 06-db-01-basics
drwxr-xr-x 2 root root 4096 дек  9 15:51 06-db-02-sql
drwxr-xr-x 2 root root 4096 дек  9 15:51 06-db-04-postgresql
drwxr-xr-x 3 root root 4096 дек  9 15:51 06-db-06-troobleshooting
-rw-r--r-- 1 root root 3283 дек  9 15:51 README.md
root@PC-Ubuntu:~/netology-project/2-virt-admin# 
root@PC-Ubuntu:~/netology-project/2-virt-admin# cd 05-virt-04
-bash: cd: 05-virt-04: Нет такого файла или каталога
root@PC-Ubuntu:~/netology-project/2-virt-admin# cd 05-virt-04-docker-compose/
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# ls -lha
итого 24K
drwxr-xr-x  5 root root 4,0K дек  9 15:51 .
drwxr-xr-x 11 root root 4,0K дек  9 15:51 ..
drwxr-xr-x  2 root root 4,0K дек  9 15:51 img
drwxr-xr-x  3 root root 4,0K дек  9 15:51 Lecture
-rw-r--r--  1 root root 2,0K дек  9 15:51 README.md
drwxr-xr-x  5 root root 4,0K дек  9 15:51 src
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# cd src
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose/src# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose/src# ls -lha
итого 20K
drwxr-xr-x 5 root root 4,0K дек  9 15:51 .
drwxr-xr-x 5 root root 4,0K дек  9 15:51 ..
drwxr-xr-x 3 root root 4,0K дек  9 15:51 ansible
drwxr-xr-x 2 root root 4,0K дек  9 15:51 packer
drwxr-xr-x 2 root root 4,0K дек  9 15:51 terraform
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose/src# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose/src# cd ..
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# ls -l
итого 16
drwxr-xr-x 2 root root 4096 дек  9 15:51 img
drwxr-xr-x 3 root root 4096 дек  9 15:51 Lecture
-rw-r--r-- 1 root root 1947 дек  9 15:51 README.md
drwxr-xr-x 5 root root 4096 дек  9 15:51 src
```
```bash
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# cp -r src ~/netology-project/Docker-Compose/
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# 
root@PC-Ubuntu:~/netology-project/2-virt-admin/05-virt-04-docker-compose# cd ~/netology-project/Docker-Compose/
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# ls -l
итого 4
drwxr-xr-x 5 root root 4096 дек  9 15:54 src
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# 
root@PC-Ubuntu:~/netology-project/Docker-Compose# cd src/
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# ls -l
итого 12
drwxr-xr-x 3 root root 4096 дек  9 15:54 ansible
drwxr-xr-x 2 root root 4096 дек  9 15:54 packer
drwxr-xr-x 2 root root 4096 дек  9 15:54 terraform
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# cd ansible/
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# ls -l
итого 16
-rw-r--r-- 1 root root   99 дек  9 15:54 ansible.cfg
-rw-r--r-- 1 root root   72 дек  9 15:54 inventory
-rw-r--r-- 1 root root 1744 дек  9 15:54 provision.yml
drwxr-xr-x 7 root root 4096 дек  9 15:54 stack
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# mc

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 

```
### Готовы к дальнейшей работе 
```bash
maestro@PC-Ubuntu:~$ sudo -i
[sudo] пароль для maestro: 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# ls -lha
итого 92K
drwx------ 13 root root 4,0K дек  9 15:45  .
drwxr-xr-x 20 root root 4,0K дек  5 13:06  ..
drwxr-xr-x  4 root root 4,0K дек  5 16:23  .ansible
-rw-------  1 root root 5,0K дек  7 21:29  .bash_history
-rw-r--r--  1 root root 3,1K дек  5  2019  .bashrc
drwx------  3 root root 4,0K дек  5 14:22  .cache
drwx------  6 root root 4,0K дек  6 21:37  .config
-rw-r--r--  1 root root   62 дек  9 15:45  .gitconfig
drwx------  3 root root 4,0K дек  5 14:22  .local
drwxr-xr-x  5 root root 4,0K дек  9 15:51  netology-project
-rw-r--r--  1 root root  161 дек  5  2019  .profile
drwxr-xr-x  3 root root 4,0K дек  5 13:14  snap
drwx------  2 root root 4,0K дек  5 16:15  .ssh
drwxr-xr-x  7 root root 4,0K дек  8 20:11  .vagrant.d
drwxr-xr-x  4 root root 4,0K дек  5 15:48  vagrant-project
-rw-------  1 root root  16K дек  5 18:20  .viminfo
drwx------  5 root root 4,0K дек  5 18:20 'VirtualBox VMs'
-rw-r--r--  1 root root  173 дек  5 13:41  .wget-hsts
drwxr-xr-x  4 root root 4,0K дек  6 21:37  .wine
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
### Устанавливаем docker-compose
```bash
root@PC-Ubuntu:~# curl -L https://github.com/docker/compose/releases/download/v2.2.2/docker-compose-linux-x86_64 `uname -s`-`uname -m` -o /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   664  100   664    0     0   1185      0 --:--:-- --:--:-- --:--:--  1185
100 23.5M  100 23.5M    0     0  1442k      0  0:00:16  0:00:16 --:--:-- 1922k
curl: (6) Could not resolve host: Linux-x86_64
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# type docker-compose
docker-compose является /usr/bin/docker-compose
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# whereis docker-compose
docker-compose: /usr/bin/docker-compose
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
### Устанавливаем утилиту "yc" Yandex.Cloud
```bash
root@PC-Ubuntu:~# curl https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  9739  100  9739    0     0   5852      0  0:00:01  0:00:01 --:--:--  5849
Downloading yc 0.85.0
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 79.7M  100 79.7M    0     0   283k      0  0:04:48  0:04:48 --:--:-- 1845k
Yandex.Cloud CLI 0.85.0 linux/amd64

yc PATH has been added to your '/root/.bashrc' profile
yc bash completion has been added to your '/root/.bashrc' profile.
Now we have zsh completion. Type "echo 'source /root/yandex-cloud/completion.zsh.inc' >>  ~/.zshrc" to install itTo complete installation, start a new shell (exec -l $SHELL) or type 'source "/root/.bashrc"' in the current one
root@PC-Ubuntu:~# 
```
#### Перечитать файл .bashrc
```bash
root@PC-Ubuntu:~# source .bashrc

```
#### Проверяем версию утилиты yc
```bash
root@PC-Ubuntu:~# yc --version
Yandex.Cloud CLI 0.85.0 linux/amd64
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# docker --verson

Команда «docker» не найдена, но может быть установлена с помощью:

snap install docker     # version 20.10.8, or
apt  install docker.io  # version 20.10.7-0ubuntu5~20.04.2

See 'snap info docker' for additional versions.

root@PC-Ubuntu:~# 
```
#### Помощь по работе утилиты
```ps
root@PC-Ubuntu:~# yc --help
Command line interface helps you interact with Yandex.Cloud services

Usage:
  yc <group|command>

Groups:
  iam                       Manage Yandex Identity and Access Manager resources
  resource-manager          Manage Yandex Resource Manager resources
  compute                   Manage Yandex Compute Cloud resources
  vpc                       Manage Yandex Virtual Private Cloud resources
  dns                       Manage Yandex DNS resources
  managed-kubernetes        Manage Kubernetes clusters.
  ydb                       Manage YDB databases.
  kms                       Manage Yandex Key Management Service resources
  cdn                       Manage CDN resources
  certificate-manager       Manage Certificate Manager resources
  managed-clickhouse        Manage ClickHouse clusters, hosts, databases, backups, users and ml-models.
  managed-mongodb           Manage MongoDB clusters, hosts, databases, backups and users.
  managed-mysql             Manage MySQL clusters, hosts, databases, backups and users.
  managed-sqlserver         Manage SQLServer clusters, databases, backups and users.
  managed-postgresql        Manage PostgreSQL clusters, hosts, databases, backups and users.
  managed-redis             Manage Redis clusters, hosts, databases, backups and users.
  managed-elasticsearch     Manage ElasticSearch clusters, hosts, indexes and backups.
  managed-kafka             Manage Apache Kafka clusters, brokers, topics and users.
  container                 Manage Container resources.
  load-balancer             Manage Yandex Load Balancer resources
  datatransfer              Manage Data Transfer endpoints and transfers
  operation                 Manage operations
  config                    Manage Yandex.Cloud CLI configuration
  components                Manage installed components
  serverless                Manage Serverless resources.
  iot                       Manage Yandex IoT Core resources
  dataproc                  Manage data processing clusters.
  application-load-balancer [PREVIEW] Manage Yandex Application Load Balancer resources
  logging                   [PREVIEW] Manage Yandex Cloud Logging
  lockbox                   [PREVIEW] Manage Yandex Lockbox resources
  organization-manager      Manage Yandex Organization Manager resources

Commands:
  init                      CLI initialization
  version                   Display Yandex.Cloud CLI version.
  help                      Help about any command

Flags:
      --profile string 
              Set the custom configuration file. 

      --debug 
              Debug logging. 

      --debug-grpc 
              Debug gRPC logging. Very verbose, used for debugging connection problems. 

      --no-user-output 
              Disable printing user intended output to stderr. 

      --retry int 
              Enable gRPC retries. By default, retries are enabled with maximum 5 attempts. 

              Pass 0 to disable retries. Pass any negative value for infinite retries. 

              Even infinite retries are capped with 2 minutes timeout. 

      --cloud-id string 
              Set the ID of the cloud to use. 

      --folder-id string 
              Set the ID of the folder to use. 

      --folder-name string 
              Set the name of the folder to use (will be resolved to id). 

      --token string 
              Set the OAuth token to use. 

      --format string 
              Set the output format: text (default), yaml, json, json-rest. 

  -h, --help 
              Display help for the command. 

  -v, --version 
              Display Yandex.Cloud CLI version.

root@PC-Ubuntu:~# 

```

### Регистрация в сервисе Cloud.Yandex
- создание аккаунта
- создание платежного аккаунта
- использование промокода от Нетологии
#### Инициализация сервиса Cloud.Yandex
```bash
root@PC-Ubuntu:~# yc init
Welcome! This command will take you through the configuration process.
Please go to https://oauth.yandex.ru/authorize?response_type=token&client_id=1a6990aa636648e9b2ef855fa7bec2fb in order to obtain OAuth token.

Please enter OAuth token: ^C
root@PC-Ubuntu:~# 
```
##### Неудачная инициализация, т.к. не был создан платедный аакаунт насервисе Cloud.Yandex
```bash
root@PC-Ubuntu:~# yc init
Welcome! This command will take you through the configuration process.
Pick desired action:
 [1] Re-initialize this profile 'default' with new settings 
 [2] Create a new profile
Please enter your numeric choice: 2
Enter profile name. Names start with a lower case letter and contain only lower case letters a-z, digits 0-9, and hyphens '-': netology
Please go to https://oauth.yandex.ru/authorize?response_type=token&client_id=1a6990aa636648e9b2ef855fa7bec2fb in order to obtain OAuth token.

Please enter OAuth token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
You have one cloud available: 'cloud-serjent' (id = b1g220k55v5cktv4kfki). It is going to be used by default.
Please choose folder to use:
 [1] default (id = b1ggdhpqn2g4ts7rsvfj)
 [2] Create a new folder
Please enter your numeric choice: 2
Please enter a folder name: netology
ERROR: Folder creation failed: rpc error: code = PermissionDenied desc = Permission denied


client-trace-id: dfe9e8c2-6931-4709-8c72-b0ba860c0f50

Use client-trace-id for investigation of issues in cloud support
If you are going to ask for help of cloud support, please send the following trace file: /root/.config/yandex-cloud/logs/2021-12-09T18-04-38.110-yc_init.txt
root@PC-Ubuntu:~# 
```
#### Успешная инициализация утилиты "yc" от Cloud.Yandex
```bash
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# yc init
Welcome! This command will take you through the configuration process.
Pick desired action:
 [1] Re-initialize this profile 'netology' with new settings 
 [2] Create a new profile
 [3] Switch to and re-initialize existing profile: 'default'
Please enter your numeric choice: 1
Please go to https://oauth.yandex.ru/authorize?response_type=token&client_id=1a6990aa636648e9b2ef855fa7bec2fb in order to obtain OAuth token.

Please enter OAuth token: [AQAAAAACD*********************jdhr2jd4s] AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
You have one cloud available: 'cloud-serjent' (id = b1g220k55v5cktv4kfki). It is going to be used by default.
Please choose folder to use:
 [1] default (id = b1ggdhpqn2g4ts7rsvfj)
 [2] Create a new folder
Please enter your numeric choice: 2
Please enter a folder name: netology-alfa
Your current folder has been set to 'netology-alfa' (id = b1gd3hm4niaifoa8dahm).
Do you want to configure a default Compute zone? [Y/n] y
Which zone do you want to use as a profile default?
 [1] ru-central1-a
 [2] ru-central1-b
 [3] ru-central1-c
 [4] Don't set default zone
Please enter your numeric choice: 1
Your profile default Compute zone has been set to 'ru-central1-a'.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
#### Конфигурация
```bash
root@PC-Ubuntu:~# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
#### Список доступных образов
```bash
root@PC-Ubuntu:~# yc compute image list
+----+------+--------+-------------+--------+
| ID | NAME | FAMILY | PRODUCT IDS | STATUS |
+----+------+--------+-------------+--------+
+----+------+--------+-------------+--------+

root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
### Создание сети. 42 минуты 04 сек. от начала лекции
Чтобы начать сборку образа Парекром надо в ручном режиме создать сеть и подсеть
Аргументами задаем имя сети, лейбл сети, дескрипшен сети
```bash
root@PC-Ubuntu:~# yc vpc network create --name net --labels my-label=netology --description "my first network via yc"
id: enpcnmun2o4c2u90824e
folder_id: b1gd3hm4niaifoa8dahm
created_at: "2021-12-09T14:55:15Z"
name: net
description: my first network via yc
labels:
  my-label: netology
```
#### Создание подсети 
```bash
root@PC-Ubuntu:~# yc vpc subnet create --name my-subnet-a --zone ru-central1-a --range 10.1.2.0/24 --network-name net --description "my first subnet via yc"
id: e9bd698br4kj49sf418j
folder_id: b1gd3hm4niaifoa8dahm
created_at: "2021-12-09T14:57:35Z"
name: my-subnet-a
description: my first subnet via yc
network_id: enpcnmun2o4c2u90824e
zone_id: ru-central1-a
v4_cidr_blocks:
- 10.1.2.0/24

```
### Создание образа ОС в Yandex.Cloud
#### Установка утилиты Packer
```bash
root@PC-Ubuntu:~# packer --version

Команда «packer» не найдена, но может быть установлена с помощью:

snap install packer  # version 1.0.0-2, or
apt  install packer  # version 1.3.4+dfsg-4

See 'snap info packer' for additional versions.

root@PC-Ubuntu:~# 
```
```bash
root@PC-Ubuntu:~# apt  install packer
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие НОВЫЕ пакеты будут установлены:
  packer
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 11 пакетов не обновлено.
Необходимо скачать 31,8 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 149 MB.
Пол:1 https://apt.releases.hashicorp.com focal/main amd64 packer amd64 1.7.8 [31,8 MB]
Получено 31,8 MB за 41с (772 kB/s)                                                                                                                                                                           
Выбор ранее не выбранного пакета packer.
(Чтение базы данных … на данный момент установлено 218876 файлов и каталогов.)
Подготовка к распаковке …/packer_1.7.8_amd64.deb …
Распаковывается packer (1.7.8) …
Настраивается пакет packer (1.7.8) …
root@PC-Ubuntu:~# 
```
```bash
root@PC-Ubuntu:~# packer --version
1.7.8
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```
### Создание образа ОС в Yandex.Cloud 44 минуты 43 сек. от начала лекции
#### Проверяем валидность конфигурации файла ` /src/packer/centos-7-base.json ` для создания образа
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# packer validate centos-7-base.json
The configuration is valid.
```
#### Запускаем сборку образа
```bash

```
