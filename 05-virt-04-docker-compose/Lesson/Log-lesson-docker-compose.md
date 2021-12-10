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
root@PC-Ubuntu:~# curl -L https://github.com/docker/compose/releases/download/v2.2.2/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   664  100   664    0     0   2563      0 --:--:-- --:--:-- --:--:--  2563
100 23.5M  100 23.5M    0     0   764k      0  0:00:31  0:00:31 --:--:-- 1051k
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# type docker-compose
для docker-compose вычислен хэш (/usr/bin/docker-compose)
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# whereis docker-compose
docker-compose: /usr/bin/docker-compose

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
Перед началом сборки образа убедиться в том, что появились необходимые новые папки и подсети в сервисе Yandex.Cloud
А так же в конфигурационный файл добавить ID папки и подсети
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# packer build centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Using as source image: fd84cmtk4glnq12cso0d (name: "centos-7-v20211206", family: "centos-7")
==> yandex: Use provided subnet id e9bd698br4kj49sf418j
==> yandex: Creating disk...
==> yandex: Creating instance...
==> yandex: Waiting for instance with id fhmnf7r5t6j3lqha6pof to become active...
    yandex: Detected instance IP: 51.250.3.101
==> yandex: Using SSH communicator to connect: 51.250.3.101
==> yandex: Waiting for SSH to become available...
==> yandex: Connected to SSH!
==> yandex: Provisioning with shell script: /tmp/packer-shell3073292614
    yandex: Loaded plugins: fastestmirror
    yandex: Loading mirror speeds from cached hostfile
    yandex:  * base: mirror.tversu.ru
    yandex:  * extras: mirror.yandex.ru
    yandex:  * updates: mirror.yandex.ru
    yandex: Resolving Dependencies
    yandex: --> Running transaction check
    yandex: ---> Package nss.x86_64 0:3.67.0-3.el7_9 will be updated
    yandex: ---> Package nss.x86_64 0:3.67.0-4.el7_9 will be an update
    yandex: ---> Package nss-sysinit.x86_64 0:3.67.0-3.el7_9 will be updated
    yandex: ---> Package nss-sysinit.x86_64 0:3.67.0-4.el7_9 will be an update
    yandex: ---> Package nss-tools.x86_64 0:3.67.0-3.el7_9 will be updated
    yandex: ---> Package nss-tools.x86_64 0:3.67.0-4.el7_9 will be an update
    yandex: --> Finished Dependency Resolution
    yandex:
    yandex: Dependencies Resolved
    yandex:
    yandex: ================================================================================
    yandex:  Package            Arch          Version                  Repository      Size
    yandex: ================================================================================
    yandex: Updating:
    yandex:  nss                x86_64        3.67.0-4.el7_9           updates        882 k
    yandex:  nss-sysinit        x86_64        3.67.0-4.el7_9           updates         66 k
    yandex:  nss-tools          x86_64        3.67.0-4.el7_9           updates        549 k
    yandex:
    yandex: Transaction Summary
    yandex: ================================================================================
    yandex: Upgrade  3 Packages
    yandex:
    yandex: Total download size: 1.5 M
    yandex: Downloading packages:
    yandex: Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
    yandex: --------------------------------------------------------------------------------
    yandex: Total                                               11 MB/s | 1.5 MB  00:00
    yandex: Running transaction check
    yandex: Running transaction test
    yandex: Transaction test succeeded
    yandex: Running transaction
    yandex:   Updating   : nss-sysinit-3.67.0-4.el7_9.x86_64                            1/6
    yandex:   Updating   : nss-3.67.0-4.el7_9.x86_64                                    2/6
    yandex:   Updating   : nss-tools-3.67.0-4.el7_9.x86_64                              3/6
    yandex:   Cleanup    : nss-tools-3.67.0-3.el7_9.x86_64                              4/6
    yandex:   Cleanup    : nss-sysinit-3.67.0-3.el7_9.x86_64                            5/6
    yandex:   Cleanup    : nss-3.67.0-3.el7_9.x86_64                                    6/6
    yandex:   Verifying  : nss-3.67.0-4.el7_9.x86_64                                    1/6
    yandex:   Verifying  : nss-sysinit-3.67.0-4.el7_9.x86_64                            2/6
    yandex:   Verifying  : nss-tools-3.67.0-4.el7_9.x86_64                              3/6
    yandex:   Verifying  : nss-tools-3.67.0-3.el7_9.x86_64                              4/6
    yandex:   Verifying  : nss-sysinit-3.67.0-3.el7_9.x86_64                            5/6
    yandex:   Verifying  : nss-3.67.0-3.el7_9.x86_64                                    6/6
    yandex:
    yandex: Updated:
    yandex:   nss.x86_64 0:3.67.0-4.el7_9           nss-sysinit.x86_64 0:3.67.0-4.el7_9
    yandex:   nss-tools.x86_64 0:3.67.0-4.el7_9
    yandex:
    yandex: Complete!
    yandex: Loaded plugins: fastestmirror
    yandex: Loading mirror speeds from cached hostfile
    yandex:  * base: mirror.tversu.ru
    yandex:  * extras: mirror.yandex.ru
    yandex:  * updates: mirror.yandex.ru
    yandex: Package iptables-1.4.21-35.el7.x86_64 already installed and latest version
    yandex: Package curl-7.29.0-59.el7_9.1.x86_64 already installed and latest version
    yandex: Package net-tools-2.0-0.25.20131004git.el7.x86_64 already installed and latest version
    yandex: Package rsync-3.1.2-10.el7.x86_64 already installed and latest version
    yandex: Package openssh-server-7.4p1-22.el7_9.x86_64 already installed and latest version
    yandex: Resolving Dependencies
    yandex: --> Running transaction check
    yandex: ---> Package bind-utils.x86_64 32:9.11.4-26.P2.el7_9.8 will be installed
    yandex: --> Processing Dependency: bind-libs-lite(x86-64) = 32:9.11.4-26.P2.el7_9.8 for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: bind-libs(x86-64) = 32:9.11.4-26.P2.el7_9.8 for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: liblwres.so.160()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libisccfg.so.160()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libisc.so.169()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libirs.so.160()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libdns.so.1102()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libbind9.so.160()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: --> Processing Dependency: libGeoIP.so.1()(64bit) for package: 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64
    yandex: ---> Package bridge-utils.x86_64 0:1.5-9.el7 will be installed
    yandex: ---> Package tcpdump.x86_64 14:4.9.2-4.el7_7.1 will be installed
    yandex: --> Processing Dependency: libpcap >= 14:1.5.3-10 for package: 14:tcpdump-4.9.2-4.el7_7.1.x86_64
    yandex: --> Processing Dependency: libpcap.so.1()(64bit) for package: 14:tcpdump-4.9.2-4.el7_7.1.x86_64
    yandex: ---> Package telnet.x86_64 1:0.17-66.el7 will be installed
    yandex: --> Running transaction check
    yandex: ---> Package GeoIP.x86_64 0:1.5.0-14.el7 will be installed
    yandex: --> Processing Dependency: geoipupdate for package: GeoIP-1.5.0-14.el7.x86_64
    yandex: ---> Package bind-libs.x86_64 32:9.11.4-26.P2.el7_9.8 will be installed
    yandex: --> Processing Dependency: bind-license = 32:9.11.4-26.P2.el7_9.8 for package: 32:bind-libs-9.11.4-26.P2.el7_9.8.x86_64
    yandex: ---> Package bind-libs-lite.x86_64 32:9.11.4-26.P2.el7_9.8 will be installed
    yandex: ---> Package libpcap.x86_64 14:1.5.3-12.el7 will be installed
    yandex: --> Running transaction check
    yandex: ---> Package bind-license.noarch 32:9.11.4-26.P2.el7_9.8 will be installed
    yandex: ---> Package geoipupdate.x86_64 0:2.5.0-1.el7 will be installed
    yandex: --> Finished Dependency Resolution
    yandex:
    yandex: Dependencies Resolved
    yandex:
    yandex: ================================================================================
    yandex:  Package            Arch       Version                        Repository   Size
    yandex: ================================================================================
    yandex: Installing:
    yandex:  bind-utils         x86_64     32:9.11.4-26.P2.el7_9.8        updates     261 k
    yandex:  bridge-utils       x86_64     1.5-9.el7                      base         32 k
    yandex:  tcpdump            x86_64     14:4.9.2-4.el7_7.1             base        422 k
    yandex:  telnet             x86_64     1:0.17-66.el7                  updates      64 k
    yandex: Installing for dependencies:
    yandex:  GeoIP              x86_64     1.5.0-14.el7                   base        1.5 M
    yandex:  bind-libs          x86_64     32:9.11.4-26.P2.el7_9.8        updates     157 k
    yandex:  bind-libs-lite     x86_64     32:9.11.4-26.P2.el7_9.8        updates     1.1 M
    yandex:  bind-license       noarch     32:9.11.4-26.P2.el7_9.8        updates      91 k
    yandex:  geoipupdate        x86_64     2.5.0-1.el7                    base         35 k
    yandex:  libpcap            x86_64     14:1.5.3-12.el7                base        139 k
    yandex:
    yandex: Transaction Summary
    yandex: ================================================================================
    yandex: Install  4 Packages (+6 Dependent packages)
    yandex:
    yandex: Total download size: 3.8 M
    yandex: Installed size: 9.0 M
    yandex: Downloading packages:
    yandex: --------------------------------------------------------------------------------
    yandex: Total                                              5.6 MB/s | 3.8 MB  00:00
    yandex: Running transaction check
    yandex: Running transaction test
    yandex: Transaction test succeeded
    yandex: Running transaction
    yandex:   Installing : 32:bind-license-9.11.4-26.P2.el7_9.8.noarch                 1/10
    yandex:   Installing : geoipupdate-2.5.0-1.el7.x86_64                              2/10
    yandex:   Installing : GeoIP-1.5.0-14.el7.x86_64                                   3/10
    yandex:   Installing : 32:bind-libs-lite-9.11.4-26.P2.el7_9.8.x86_64               4/10
    yandex:   Installing : 32:bind-libs-9.11.4-26.P2.el7_9.8.x86_64                    5/10
    yandex:   Installing : 14:libpcap-1.5.3-12.el7.x86_64                              6/10
    yandex: pam_tally2: Error opening /var/log/tallylog for update: Permission denied
    yandex: pam_tally2: Authentication error
    yandex: useradd: failed to reset the tallylog entry of user "tcpdump"
    yandex:   Installing : 14:tcpdump-4.9.2-4.el7_7.1.x86_64                           7/10
    yandex:   Installing : 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64                   8/10
    yandex:   Installing : bridge-utils-1.5-9.el7.x86_64                               9/10
    yandex:   Installing : 1:telnet-0.17-66.el7.x86_64                                10/10
    yandex:   Verifying  : GeoIP-1.5.0-14.el7.x86_64                                   1/10
    yandex:   Verifying  : 1:telnet-0.17-66.el7.x86_64                                 2/10
    yandex:   Verifying  : 14:libpcap-1.5.3-12.el7.x86_64                              3/10
    yandex:   Verifying  : geoipupdate-2.5.0-1.el7.x86_64                              4/10
    yandex:   Verifying  : 14:tcpdump-4.9.2-4.el7_7.1.x86_64                           5/10
    yandex:   Verifying  : 32:bind-license-9.11.4-26.P2.el7_9.8.noarch                 6/10
    yandex:   Verifying  : 32:bind-libs-lite-9.11.4-26.P2.el7_9.8.x86_64               7/10
    yandex:   Verifying  : 32:bind-utils-9.11.4-26.P2.el7_9.8.x86_64                   8/10
    yandex:   Verifying  : 32:bind-libs-9.11.4-26.P2.el7_9.8.x86_64                    9/10
    yandex:   Verifying  : bridge-utils-1.5-9.el7.x86_64                              10/10
    yandex:
    yandex: Installed:
    yandex:   bind-utils.x86_64 32:9.11.4-26.P2.el7_9.8   bridge-utils.x86_64 0:1.5-9.el7
    yandex:   tcpdump.x86_64 14:4.9.2-4.el7_7.1           telnet.x86_64 1:0.17-66.el7
    yandex:
    yandex: Dependency Installed:
    yandex:   GeoIP.x86_64 0:1.5.0-14.el7
    yandex:   bind-libs.x86_64 32:9.11.4-26.P2.el7_9.8
    yandex:   bind-libs-lite.x86_64 32:9.11.4-26.P2.el7_9.8
    yandex:   bind-license.noarch 32:9.11.4-26.P2.el7_9.8
    yandex:   geoipupdate.x86_64 0:2.5.0-1.el7
    yandex:   libpcap.x86_64 14:1.5.3-12.el7
    yandex:
    yandex: Complete!
==> yandex: Stopping instance...
==> yandex: Deleting instance...
    yandex: Instance has been deleted!
==> yandex: Creating image: centos-7-base
==> yandex: Waiting for image to complete...
==> yandex: Success image create...
==> yandex: Destroying boot disk...
    yandex: Disk has been deleted!
Build 'yandex' finished after 4 minutes 5 seconds.

==> Wait completed after 4 minutes 5 seconds

==> Builds finished. The artifacts of successful builds are:
--> yandex: A disk image was created: centos-7-base (id: fd87ftkus6nii1k3epnu) with family name centos
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
```
[Результат](/05-virt-04-docker-compose/img/new-images-in-yandex-cloud.png)
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# yc compute image list
+----------------------+---------------+--------+----------------------+--------+
|          ID          |     NAME      | FAMILY |     PRODUCT IDS      | STATUS |
+----------------------+---------------+--------+----------------------+--------+
| fd87ftkus6nii1k3epnu | centos-7-base | centos | f2e1me997vtfd7aa3hb3 | READY  |
+----------------------+---------------+--------+----------------------+--------+

```
#### Ошибки при создании образа
- нет авторизации платного аккаунта
- утилита yc должна быть доступна из папки, где запускается Packer
```bash
root@PC-Ubuntu:~# packer build /root/netology-project/Docker-Compose/src/packer/centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Error getting source image for instance creation: client-request-id = 90dc131f-8281-4403-b1e4-f6d4f2d9c1ee client-trace-id = 7a9e53fa-1860-43ab-b5d2-741128428173 rpc error: code = Unauthenticated desc = iam token create failed: failed to get compute instance service account token from instance metadata service: GET http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token: Get "http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token": dial tcp 169.254.169.254:80: i/o timeout.
==> yandex: Are you inside compute instance?
Build 'yandex' errored after 1 second 863 milliseconds: Error getting source image for instance creation: client-request-id = 90dc131f-8281-4403-b1e4-f6d4f2d9c1ee client-trace-id = 7a9e53fa-1860-43ab-b5d2-741128428173 rpc error: code = Unauthenticated desc = iam token create failed: failed to get compute instance service account token from instance metadata service: GET http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token: Get "http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token": dial tcp 169.254.169.254:80: i/o timeout.
Are you inside compute instance?

==> Wait completed after 1 second 864 milliseconds

==> Some builds didn't complete successfully and had errors:
--> yandex: Error getting source image for instance creation: client-request-id = 90dc131f-8281-4403-b1e4-f6d4f2d9c1ee client-trace-id = 7a9e53fa-1860-43ab-b5d2-741128428173 rpc error: code = Unauthenticated desc = iam token create failed: failed to get compute instance service account token from instance metadata service: GET http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token: Get "http://169.254.169.254/computeMetadata/v1/instance/service-accounts/default/token": dial tcp 169.254.169.254:80: i/o timeout.
Are you inside compute instance?

==> Builds finished but no artifacts were created.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# packer validate /root/netology-project/Docker-Compose/src/packer/centos-7-base.json
The configuration is valid.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cd /root/netology-project/Docker-Compose/src
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# cd
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# packer validate /root/netology-project/Docker-Compose/src/packer/centos-7-base.json
The configuration is valid.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# packer build /root/netology-project/Docker-Compose/src/packer/centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Using as source image: fd84cmtk4glnq12cso0d (name: "centos-7-v20211206", family: "centos-7")
==> yandex: Use provided subnet id enpcnmun2o4c2u90824e
==> yandex: Creating disk...
==> yandex: Error creating disk: server-request-id = ffe308ad-51bd-46ee-bccf-e9c643513fd6 server-trace-id = 65e26a491ddfa19d:fc50504e6b9540cc:65e26a491ddfa19d:1 client-request-id = 4b444301-e435-4b4d-8411-15df2dd75d2e client-trace-id = 1c3798d1-b296-4185-a914-d1ac3ef420a9 rpc error: code = PermissionDenied desc = Permission denied to folder b1gaec42k169jqpo02f7
Build 'yandex' errored after 1 second 339 milliseconds: Error creating disk: server-request-id = ffe308ad-51bd-46ee-bccf-e9c643513fd6 server-trace-id = 65e26a491ddfa19d:fc50504e6b9540cc:65e26a491ddfa19d:1 client-request-id = 4b444301-e435-4b4d-8411-15df2dd75d2e client-trace-id = 1c3798d1-b296-4185-a914-d1ac3ef420a9 rpc error: code = PermissionDenied desc = Permission denied to folder b1gaec42k169jqpo02f7

==> Wait completed after 1 second 339 milliseconds

==> Some builds didn't complete successfully and had errors:
--> yandex: Error creating disk: server-request-id = ffe308ad-51bd-46ee-bccf-e9c643513fd6 server-trace-id = 65e26a491ddfa19d:fc50504e6b9540cc:65e26a491ddfa19d:1 client-request-id = 4b444301-e435-4b4d-8411-15df2dd75d2e client-trace-id = 1c3798d1-b296-4185-a914-d1ac3ef420a9 rpc error: code = PermissionDenied desc = Permission denied to folder b1gaec42k169jqpo02f7

==> Builds finished but no artifacts were created.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# packer --version
1.7.8
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# packer build /root/netology-project/Docker-Compose/src/packer/centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Using as source image: fd84cmtk4glnq12cso0d (name: "centos-7-v20211206", family: "centos-7")
==> yandex: Use provided subnet id enpcnmun2o4c2u90824e
==> yandex: Creating disk...
==> yandex: Creating instance...
==> yandex: Error create instance: server-request-id = edf0f295-6ea2-454e-9cb9-9eed15e977f6 server-trace-id = dacfc8c2b701566:22107c63e0ea79e2:dacfc8c2b701566:1 client-request-id = 10724ebc-7bbc-4260-91e0-a5f6fd731d25 client-trace-id = 6f1687e7-a802-489f-bc96-b01897039020 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found
==> yandex: Destroying boot disk...
    yandex: Disk has been deleted!
Build 'yandex' errored after 13 seconds 918 milliseconds: Error create instance: server-request-id = edf0f295-6ea2-454e-9cb9-9eed15e977f6 server-trace-id = dacfc8c2b701566:22107c63e0ea79e2:dacfc8c2b701566:1 client-request-id = 10724ebc-7bbc-4260-91e0-a5f6fd731d25 client-trace-id = 6f1687e7-a802-489f-bc96-b01897039020 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Wait completed after 13 seconds 918 milliseconds

==> Some builds didn't complete successfully and had errors:
--> yandex: Error create instance: server-request-id = edf0f295-6ea2-454e-9cb9-9eed15e977f6 server-trace-id = dacfc8c2b701566:22107c63e0ea79e2:dacfc8c2b701566:1 client-request-id = 10724ebc-7bbc-4260-91e0-a5f6fd731d25 client-trace-id = 6f1687e7-a802-489f-bc96-b01897039020 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Builds finished but no artifacts were created.
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# type yc
для yc вычислен хэш (/root/yandex-cloud/bin/yc)
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cd /root/netology-project/Docker-Compose/src/
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# type yc
для yc вычислен хэш (/root/yandex-cloud/bin/yc)
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# cd packer/
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# type yc
для yc вычислен хэш (/root/yandex-cloud/bin/yc)
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# packer build centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Using as source image: fd84cmtk4glnq12cso0d (name: "centos-7-v20211206", family: "centos-7")
==> yandex: Use provided subnet id enpcnmun2o4c2u90824e
==> yandex: Creating disk...
==> yandex: Creating instance...
==> yandex: Error create instance: server-request-id = ec54555b-18d4-45a9-b28e-22f866cd02e2 server-trace-id = 84d5356d8d6fccf4:6d0f8e4f119e18bb:84d5356d8d6fccf4:1 client-request-id = d00ebdf5-4260-446f-9af5-4e363537f48a client-trace-id = 7f42886f-8893-4453-9b0d-4620a2db5073 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found
==> yandex: Destroying boot disk...
    yandex: Disk has been deleted!
Build 'yandex' errored after 8 seconds 201 milliseconds: Error create instance: server-request-id = ec54555b-18d4-45a9-b28e-22f866cd02e2 server-trace-id = 84d5356d8d6fccf4:6d0f8e4f119e18bb:84d5356d8d6fccf4:1 client-request-id = d00ebdf5-4260-446f-9af5-4e363537f48a client-trace-id = 7f42886f-8893-4453-9b0d-4620a2db5073 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Wait completed after 8 seconds 201 milliseconds

==> Some builds didn't complete successfully and had errors:
--> yandex: Error create instance: server-request-id = ec54555b-18d4-45a9-b28e-22f866cd02e2 server-trace-id = 84d5356d8d6fccf4:6d0f8e4f119e18bb:84d5356d8d6fccf4:1 client-request-id = d00ebdf5-4260-446f-9af5-4e363537f48a client-trace-id = 7f42886f-8893-4453-9b0d-4620a2db5073 rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Builds finished but no artifacts were created.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# cd ..
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc init
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
 [2] netology-alfa (id = b1gd3hm4niaifoa8dahm)
 [3] Create a new folder
Please enter your numeric choice: 2
Your current folder has been set to 'netology-alfa' (id = b1gd3hm4niaifoa8dahm).
Do you want to configure a default Compute zone? [Y/n] n
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc init
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
 [2] netology-alfa (id = b1gd3hm4niaifoa8dahm)
 [3] Create a new folder
Please enter your numeric choice: 2
Your current folder has been set to 'netology-alfa' (id = b1gd3hm4niaifoa8dahm).
Do you want to configure a default Compute zone? [Y/n] y
Which zone do you want to use as a profile default?
 [1] ru-central1-a
 [2] ru-central1-b
 [3] ru-central1-c
 [4] Don't set default zone
Please enter your numeric choice: 1
Your profile default Compute zone has been set to 'ru-central1-a'.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc vpc network create --name net --labels my-label=netology --description "my first network via yc"
ERROR: rpc error: code = ResourceExhausted desc = Quota limit vpc.networks.count exceeded


server-request-id: bc79c486-5ca1-43e6-a705-05049076805f
client-request-id: fd7e2c80-e621-4cf2-bf69-8266245863c8
server-trace-id: 7cdbd258622e1b94:9fefaa671d0491c1:7cdbd258622e1b94:1
client-trace-id: 86f0ead6-d044-4f14-a0b3-ce6edc1e3d73

Use server-request-id, client-request-id, server-trace-id, client-trace-id for investigation of issues in cloud support
If you are going to ask for help of cloud support, please send the following trace file: /root/.config/yandex-cloud/logs/2021-12-09T20-40-44.533-yc_vpc_network_create.txt
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# yc vpc network create --name net --labels my-label=netology --description "my first network via yc"
ERROR: rpc error: code = ResourceExhausted desc = Quota limit vpc.networks.count exceeded


server-request-id: dda1c014-2186-44aa-beea-f69f705e3d24
client-request-id: ed7fa22e-e2ba-442a-abf1-8530977fb408
server-trace-id: ef45ee6560f658bf:864b2a74e38c18f3:ef45ee6560f658bf:1
client-trace-id: e6ec0629-3723-4750-ab57-148a89221f4f

Use server-request-id, client-request-id, server-trace-id, client-trace-id for investigation of issues in cloud support
If you are going to ask for help of cloud support, please send the following trace file: /root/.config/yandex-cloud/logs/2021-12-09T20-44-47.925-yc_vpc_network_create.txt
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# packer build centos-7-base.json
"centos-7-base.json": stat centos-7-base.json: no such file or directory
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# cd packer/
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# packer build centos-7-base.json
yandex: output will be in this color.

==> yandex: Creating temporary ssh key for instance...
==> yandex: Using as source image: fd84cmtk4glnq12cso0d (name: "centos-7-v20211206", family: "centos-7")
==> yandex: Use provided subnet id enpcnmun2o4c2u90824e
==> yandex: Creating disk...
==> yandex: Creating instance...
==> yandex: Error create instance: server-request-id = 2d0f6d77-86c6-4eaa-9bf2-a30cfc878c70 server-trace-id = 430b45d6e3eef866:bbfbf554734bbbe1:430b45d6e3eef866:1 client-request-id = 16dda504-6620-4368-9d65-a6c6e57286b8 client-trace-id = 431e0521-6e01-47d1-be7d-c5bbd275436a rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found
==> yandex: Destroying boot disk...
    yandex: Disk has been deleted!
Build 'yandex' errored after 6 seconds 854 milliseconds: Error create instance: server-request-id = 2d0f6d77-86c6-4eaa-9bf2-a30cfc878c70 server-trace-id = 430b45d6e3eef866:bbfbf554734bbbe1:430b45d6e3eef866:1 client-request-id = 16dda504-6620-4368-9d65-a6c6e57286b8 client-trace-id = 431e0521-6e01-47d1-be7d-c5bbd275436a rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Wait completed after 6 seconds 854 milliseconds

==> Some builds didn't complete successfully and had errors:
--> yandex: Error create instance: server-request-id = 2d0f6d77-86c6-4eaa-9bf2-a30cfc878c70 server-trace-id = 430b45d6e3eef866:bbfbf554734bbbe1:430b45d6e3eef866:1 client-request-id = 16dda504-6620-4368-9d65-a6c6e57286b8 client-trace-id = 431e0521-6e01-47d1-be7d-c5bbd275436a rpc error: code = NotFound desc = Subnet enpcnmun2o4c2u90824e not found

==> Builds finished but no artifacts were created.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/packer# 

```
##### неверно указаны ID папки и подсети
```bash

```
### Terraform 1 час 48 сек. от начала лекции
#### Установка Terraform
https://www.terraform.io/docs/cli/install/apt.html
##### Добавляем ключ для репозитория
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK

```
##### Добавляем репозиторий
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]                                                                                                               
Сущ:3 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]                                                                                                                                 
Сущ:5 https://dl.google.com/linux/chrome/deb stable InRelease                                                                                                                                       
Сущ:6 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                                                                          
Пол:7 https://apt.releases.hashicorp.com focal InRelease [9 495 B]                                                        
Пол:8 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                 
Пол:9 http://ru.archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [572 kB]
Пол:10 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1 391 kB]
Пол:11 https://apt.releases.hashicorp.com focal/main amd64 Packages [38,2 kB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal-updates/main Translation-en [282 kB]                      
Пол:13 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 DEP-11 Metadata [278 kB]               
Пол:14 http://security.ubuntu.com/ubuntu focal-security/main amd64 DEP-11 Metadata [35,7 kB]                 
Пол:15 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [881 kB]                        
Пол:16 http://security.ubuntu.com/ubuntu focal-security/universe i386 Packages [523 kB]                          
Пол:17 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe i386 Packages [652 kB]
Пол:18 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [665 kB]     
Пол:19 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [191 kB]    
Пол:20 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 DEP-11 Metadata [361 kB]   
Пол:21 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [19,6 kB]          
Пол:22 http://ru.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 DEP-11 Metadata [940 B]            
Пол:23 http://ru.archive.ubuntu.com/ubuntu focal-backports/main amd64 DEP-11 Metadata [7 988 B]            
Пол:24 http://ru.archive.ubuntu.com/ubuntu focal-backports/universe amd64 DEP-11 Metadata [11,3 kB]               
Пол:25 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [111 kB]                       
Пол:26 http://security.ubuntu.com/ubuntu focal-security/universe amd64 DEP-11 Metadata [64,6 kB]
Пол:27 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [12,9 kB]
Пол:28 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 DEP-11 Metadata [2 464 B]
Получено 6 445 kB за 4с (1 542 kB/s)                                       
Чтение списков пакетов… Готово
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «https://dl.google.com/linux/chrome/deb stable InRelease» не поддерживает архитектуру «i386»
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 

```
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# dpkg --print-architecture 
amd64
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
```
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# lsb_release -cs
focal
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
```
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# apt update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease                                                                                                                                            
Сущ:3 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Сущ:4 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                                                                                                                                          
Пол:5 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                                                                                                    
Сущ:6 https://dl.google.com/linux/chrome/deb stable InRelease                                                                                                                                
Сущ:7 https://apt.releases.hashicorp.com focal InRelease                                                                                                                           
Сущ:8 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                           
Получено 114 kB за 2с (59,8 kB/s)                                          
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Может быть обновлено 13 пакетов. Запустите «apt list --upgradable» для их показа.
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «https://dl.google.com/linux/chrome/deb stable InRelease» не поддерживает архитектуру «i386»
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
```
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# apt install terraform
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие НОВЫЕ пакеты будут установлены:
  terraform
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 13 пакетов не обновлено.
Необходимо скачать 18,7 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 61,9 MB.
Пол:1 https://apt.releases.hashicorp.com focal/main amd64 terraform amd64 1.1.0 [18,7 MB]
Получено 18,7 MB за 12с (1 571 kB/s)                                                                                                                                                                         
Выбор ранее не выбранного пакета terraform.
(Чтение базы данных … на данный момент установлено 218879 файлов и каталогов.)
Подготовка к распаковке …/terraform_1.1.0_amd64.deb …
Распаковывается terraform (1.1.0) …
Настраивается пакет terraform (1.1.0) …
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# 
```
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src# terraform --version
Terraform v1.1.0
on linux_amd64

```
## Запуск создания ВМ в облаке на основе ранее созданного образа с помощью Teraform
### Запуск Teraform
#### Инициализация Terraform
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of yandex-cloud/yandex...
- Installing yandex-cloud/yandex v0.67.0...
- Installed yandex-cloud/yandex v0.67.0 (self-signed, key ID E40F590B50BB8E40)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```
#### Проерка валидности конфигурации
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
╷
│ Error: JSON in "key.json" are not valid: invalid character 'k' looking for beginning of value
│ 
│   with provider["registry.terraform.io/yandex-cloud/yandex"],
│   on provider.tf line 11, in provider "yandex":
│   11:   service_account_key_file = "key.json"
│ 
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```
Вышла ошибка о том, что нет файла "key.json" с ключем для подключения к провайдеру Яндекс.
Решение: в файле "privider.tf" место это строки записано  "token = "AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s"
Источник решения: [В начале конфигурационного файла необходимо задать настройки провайдера.](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart#configure-provider)
#### Взяли параметры токена из конфика яндекс облака
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# yc config list
token: AQAAAAACDSBNAATuwbWrT28RHkWyvGjdhr2jd4s
cloud-id: b1g220k55v5cktv4kfki
folder-id: b1gd3hm4niaifoa8dahm
compute-default-zone: ru-central1-a
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```
#### Второй запуск валидации конфигурации Terraform
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
╷
│ Error: Invalid function argument
│ 
│   on node01.tf line 27, in resource "yandex_compute_instance" "node01":
│   27:     ssh-keys = "centos:${file("~/.ssh/id_rsa.pub")}"
│ 
│ Invalid value for "path" parameter: no file exists at ~/.ssh/id_rsa.pub; this function works only with files that are distributed as part of the configuration source code, so if this file will be created
│ by a resource in this configuration you must instead obtain this result from an attribute of that resource.
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 

```
Вышла ошибка о том, что отстутствует файл с ключем SSH на локальной системе
Решение: сгенерировать ключи SSH.
Источник решения: [1](https://tyapk.ru/blog/post/copy-ssh-public-key-to-server), [2](https://firstvds.ru/technology/dobavit-ssh-klyuch)
```bash
root@PC-Ubuntu:~# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:yZBUNVTE6Lhpup9vUFOoo7gpNkKpc8FQAFm+2ZY2Frc root@PC-Ubuntu
The key's randomart image is:
+---[RSA 3072]----+
|++.   ...o+*o    |
|...  . .  o.o    |
| .. . +  + .     |
|.  + + ++.+      |
| o+ B.E.S= .     |
| oo+... =        |
|o  . o o .       |
|+ = o .  ..      |
| = o  .ooo.      |
+----[SHA256]-----+
root@PC-Ubuntu:~# 
```
##### Ключ готов и находится в директории "~/.ssh"
```bash
root@PC-Ubuntu:~# ls -l
итого 20
drwxr-xr-x 5 root root 4096 дек  9 15:51  netology-project
drwxr-xr-x 3 root root 4096 дек  5 13:14  snap
drwxr-xr-x 4 root root 4096 дек  5 15:48  vagrant-project
drwx------ 5 root root 4096 дек  5 18:20 'VirtualBox VMs'
drwxr-xr-x 4 root root 4096 дек  9 16:49  yandex-cloud
root@PC-Ubuntu:~# ls -lha
итого 104K
drwx------ 15 root root 4,0K дек  9 22:10  .
drwxr-xr-x 20 root root 4,0K дек  5 13:06  ..
drwxr-xr-x  4 root root 4,0K дек  5 16:23  .ansible
-rw-------  1 root root 5,1K дек 10 12:32  .bash_history
-rw-r--r--  1 root root 3,4K дек  9 16:49  .bashrc
drwx------  4 root root 4,0K дек 10 14:54  .cache
drwx------  8 root root 4,0K дек  9 19:01  .config
-rw-r--r--  1 root root   62 дек  9 15:45  .gitconfig
drwx------  3 root root 4,0K дек  5 14:22  .local
drwxr-xr-x  5 root root 4,0K дек  9 15:51  netology-project
-rw-r--r--  1 root root  161 дек  5  2019  .profile
-rw-r--r--  1 root root   72 дек  9 19:58  .selected_editor
drwxr-xr-x  3 root root 4,0K дек  5 13:14  snap
drwx------  2 root root 4,0K дек 10 15:56  .ssh
drwxr-xr-x  2 root root 4,0K дек  9 22:10  .terraform.d
drwxr-xr-x  7 root root 4,0K дек  8 20:11  .vagrant.d
drwxr-xr-x  4 root root 4,0K дек  5 15:48  vagrant-project
-rw-------  1 root root  16K дек  5 18:20  .viminfo
drwx------  5 root root 4,0K дек  5 18:20 'VirtualBox VMs'
-rw-r--r--  1 root root  173 дек  5 13:41  .wget-hsts
drwxr-xr-x  4 root root 4,0K дек  6 21:37  .wine
drwxr-xr-x  4 root root 4,0K дек  9 16:49  yandex-cloud
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cd .ssh/
root@PC-Ubuntu:~/.ssh# 
root@PC-Ubuntu:~/.ssh# ls -l
итого 8
-rw------- 1 root root 2602 дек 10 15:56 id_rsa
-rw-r--r-- 1 root root  568 дек 10 15:56 id_rsa.pub
root@PC-Ubuntu:~/.ssh# cat id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
root@PC-Ubuntu:~/.ssh# 

```
#### В третий раз запускаем валидацию конфогурации Terraform
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
Success! The configuration is valid.

```
Успешно!
#### Проверяем план создания ВМ
 С плюсами - это все то, что Терраформ собирается создать
```tf
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.cloud"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node01"
      + network_acceleration_type = "standard"
      + platform_id               = "standard-v1"
      + service_account_id        = (known after apply)
      + status                    = (known after apply)
      + zone                      = "ru-central1-a"

      + boot_disk {
          + auto_delete = true
          + device_name = (known after apply)
          + disk_id     = (known after apply)
          + mode        = (known after apply)

          + initialize_params {
              + description = (known after apply)
              + image_id    = "fd8ft6norj68lo29qlpi"
              + name        = "root-node01"
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = (known after apply)
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_vpc_network.default will be created
  + resource "yandex_vpc_network" "default" {
      + created_at                = (known after apply)
      + default_security_group_id = (known after apply)
      + folder_id                 = (known after apply)
      + id                        = (known after apply)
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01_yandex_cloud = (known after apply)
  + internal_ip_address_node01_yandex_cloud = (known after apply)

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 

```
#### Редактируем файл "variables.tf"
```bash
# Заменить на ID своего облака
# https://console.cloud.yandex.ru/cloud?section=overview
variable "yandex_cloud_id" {
  default = "b1g220k55v5cktv4kfki" # - Здесь
}

# Заменить на Folder своего облака
# https://console.cloud.yandex.ru/cloud?section=overview
variable "yandex_folder_id" {
  default = "b1gd3hm4niaifoa8dahm" # - Здесь
}

# Заменить на ID своего образа
# ID можно узнать с помощью команды yc compute image list
variable "centos-7-base" {
  default = "fd87ftkus6nii1k3epnu" # - Здесь
}

```
#### Проверяем доступные ресурсы
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# yc resource-manager folder list
+----------------------+---------------+--------+--------+
|          ID          |     NAME      | LABELS | STATUS |
+----------------------+---------------+--------+--------+
| b1ggdhpqn2g4ts7rsvfj | default       |        | ACTIVE |
| b1gd3hm4niaifoa8dahm | netology-alfa |        | ACTIVE |
+----------------------+---------------+--------+--------+


```
#### Создавался сервисный аккаунт и новый профиль для создания ВМ. НО этот вариант не помог нормально запустить Терраформ
```bash

```
### Запускаем создание ВМ
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.cloud"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node01"
      + network_acceleration_type = "standard"
      + platform_id               = "standard-v1"
      + service_account_id        = (known after apply)
      + status                    = (known after apply)
      + zone                      = "ru-central1-a"

      + boot_disk {
          + auto_delete = true
          + device_name = (known after apply)
          + disk_id     = (known after apply)
          + mode        = (known after apply)

          + initialize_params {
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node01"
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = (known after apply)
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_vpc_network.default will be created
  + resource "yandex_vpc_network" "default" {
      + created_at                = (known after apply)
      + default_security_group_id = (known after apply)
      + folder_id                 = (known after apply)
      + id                        = (known after apply)
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = "enpe24e1imt3pnl2hepl"
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01_yandex_cloud = (known after apply)
  + internal_ip_address_node01_yandex_cloud = (known after apply)
yandex_vpc_network.default: Creating...
yandex_vpc_subnet.default: Creating...
yandex_vpc_subnet.default: Creation complete after 1s [id=e9bjuh1beitbgp5q3fb5]
yandex_compute_instance.node01: Creating...
yandex_vpc_network.default: Creation complete after 1s [id=enpg408972efls369k28]
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [40s elapsed]
yandex_compute_instance.node01: Creation complete after 45s [id=fhmklokig6f0516hc354]

Apply complete! Resources: 3 added, 0 changed, 0 destroyed.

Outputs:

external_ip_address_node01_yandex_cloud = "51.250.0.11"
internal_ip_address_node01_yandex_cloud = "192.168.101.27"

```
Виртуальная машина создалась. На нее можно посмотреть:
[Новая ВМ Centos](/)
##### Можно зайти на ВМ по IP адресу
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# ssh centos@51.250.0.11
The authenticity of host '51.250.0.11 (51.250.0.11)' can't be established.
ECDSA key fingerprint is SHA256:rhfZA3xNuBhDU3UC6PDTBBQMwEKDUNBNYfrYo3eMgAQ.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '51.250.0.11' (ECDSA) to the list of known hosts.
[centos@node01 ~]$ 
[centos@node01 ~]$ 
[centos@node01 ~]$ cat /etc/*release
CentOS Linux release 7.9.2009 (Core)
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

CentOS Linux release 7.9.2009 (Core)
CentOS Linux release 7.9.2009 (Core)
[centos@node01 ~]$ 

```
```bash
[centos@node01 ~]$ uptime
 17:14:53 up 21 min,  1 user,  load average: 0,00, 0,01, 0,02
[centos@node01 ~]$ 
[centos@node01 ~]$ type docker
-bash: type: docker: не найден

```
### Запускаем Деплой ПО и стека микросервисов на виртуальную машину в Yandex.Cloud 1 час 9 минут 10 сек. от начала лекции
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# ansible-playbook provision.yml 

PLAY [nodes] *************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Create directory for ssh-keys] *************************************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] **********************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Checking DNS] ******************************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Installing tools] **************************************************************************************************************************************************************************************
changed: [node01.netology.cloud] => (item=['git', 'curl'])

TASK [Add docker repository] *********************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Installing docker package] *****************************************************************************************************************************************************************************
changed: [node01.netology.cloud] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])

TASK [Enable docker daemon] **********************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Install docker-compose] ********************************************************************************************************************************************************************************
fatal: [node01.netology.cloud]: FAILED! => {"changed": true, "msg": "non-zero return code", "rc": 6, "stderr": "Shared connection to 51.250.0.11 closed.\r\n", "stderr_lines": ["Shared connection to 51.250.0.11 closed."], "stdout": "  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current\r\n                                 Dload  Upload   Total   Spent    Left  Speed\r\n\r  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0\r100   664  100   664    0     0   1453      0 --:--:-- --:--:-- --:--:--  1456\r\n\r  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0\r100 23.5M  100 23.5M    0     0  19.4M      0  0:00:01  0:00:01 --:--:-- 34.4M\r\ncurl: (6) Could not resolve host: Linux-x86_64; Неизвестная ошибка\r\n", "stdout_lines": ["  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current", "                                 Dload  Upload   Total   Spent    Left  Speed", "", "  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0", "100   664  100   664    0     0   1453      0 --:--:-- --:--:-- --:--:--  1456", "", "  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0", "100 23.5M  100 23.5M    0     0  19.4M      0  0:00:01  0:00:01 --:--:-- 34.4M", "curl: (6) Could not resolve host: Linux-x86_64; Неизвестная ошибка"]}

PLAY RECAP ***************************************************************************************************************************************************************************************************
node01.netology.cloud      : ok=8    changed=6    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 
```
##### Ошибка связана с лишним пробелом в файле privision.yml
```yml
- name: Install docker-compose
        raw: $(curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose)

# Лишний пробел был здесь: "d/1.29.2/docker-compose-[должно быть без пробелов]`uname -s`-`uname -m"
```
#### Снова запускаем ansible-playbook
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# ansible-playbook provision.yml 

PLAY [nodes] *************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Create directory for ssh-keys] *************************************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] **********************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Checking DNS] ******************************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Installing tools] **************************************************************************************************************************************************************************************
ok: [node01.netology.cloud] => (item=['git', 'curl'])

TASK [Add docker repository] *********************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Installing docker package] *****************************************************************************************************************************************************************************
ok: [node01.netology.cloud] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])

TASK [Enable docker daemon] **********************************************************************************************************************************************************************************
ok: [node01.netology.cloud]

TASK [Install docker-compose] ********************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Synchronization] ***************************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Pull all images in compose] ****************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

TASK [Up all services in compose] ****************************************************************************************************************************************************************************
changed: [node01.netology.cloud]

PLAY RECAP ***************************************************************************************************************************************************************************************************
node01.netology.cloud      : ok=12   changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
#### Заходим на созданую ВМ
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# ssh centos@51.250.0.11

```
#### Видим запущенные микросервисы
```bash
[centos@node01 ~]$ 
[centos@node01 ~]$ sudo -i
[root@node01 ~]# 
[root@node01 ~]# docker ps
CONTAINER ID   IMAGE                                       COMMAND                  CREATED         STATUS                   PORTS                                                                              NAMES
473b67a997a9   gcr.io/google-containers/cadvisor:v0.34.0   "/usr/bin/cadvisor -…"   8 minutes ago   Up 7 minutes (healthy)   8080/tcp                                                                           cadvisor
7e79c03f2570   prom/prometheus:v2.17.1                     "/bin/prometheus --c…"   8 minutes ago   Up 7 minutes             9090/tcp                                                                           prometheus
5ab790676236   grafana/grafana:7.4.2                       "/run.sh"                8 minutes ago   Up 7 minutes             3000/tcp                                                                           grafana
19c1819338f1   stefanprodan/caddy                          "/sbin/tini -- caddy…"   8 minutes ago   Up 7 minutes             0.0.0.0:3000->3000/tcp, 0.0.0.0:9090-9091->9090-9091/tcp, 0.0.0.0:9093->9093/tcp   caddy
43d02e782a70   prom/pushgateway:v1.2.0                     "/bin/pushgateway"       8 minutes ago   Up 7 minutes             9091/tcp                                                                           pushgateway
882fa1562926   prom/alertmanager:v0.20.0                   "/bin/alertmanager -…"   8 minutes ago   Up 7 minutes             9093/tcp                                                                           alertmanager
cd2c9ce3a5cb   prom/node-exporter:v0.18.1                  "/bin/node_exporter …"   8 minutes ago   Up 7 minutes             9100/tcp                                                                           nodeexporter
[root@node01 ~]# 

```
#### Проверяем чинхронизацию дирктории со стеком микросервисов
```bash
[root@node01 ~]# cd /opt/stack
[root@node01 stack]# 
[root@node01 stack]# ls -lha
итого 8,0K
drwxr-xr-x. 7 root root  128 дек 10 17:45 .
drwxr-xr-x. 4 root root   37 дек 10 17:45 ..
drwxr-xr-x. 2 root root   24 дек 10 17:45 alertmanager
drwxr-xr-x. 2 root root   23 дек 10 17:45 caddy
-rw-r--r--. 1 root root 3,0K дек 10 17:45 docker-compose.yaml
-rw-r--r--. 1 root root   38 дек 10 17:45 .env
drwxr-xr-x. 2 root root   43 дек 10 17:45 exporters
drwxr-xr-x. 3 root root   26 дек 10 17:45 grafana
drwxr-xr-x. 2 root root   47 дек 10 17:45 prometheus
[root@node01 stack]# 

```
#### Проверяем запущенные процессы Docker-compose
```bash
[root@node01 stack]# docker-compose ps
NAME                COMMAND                  SERVICE             STATUS              PORTS
alertmanager        "/bin/alertmanager -…"   alertmanager        running             9093/tcp
caddy               "/sbin/tini -- caddy…"   caddy               running             0.0.0.0:3000->3000/tcp, 0.0.0.0:9090-9091->9090-9091/tcp, 0.0.0.0:9093->9093/tcp
cadvisor            "/usr/bin/cadvisor -…"   cadvisor            running (healthy)   8080/tcp
grafana             "/run.sh"                grafana             running             3000/tcp
nodeexporter        "/bin/node_exporter …"   nodeexporter        running             9100/tcp
prometheus          "/bin/prometheus --c…"   prometheus          running             9090/tcp
pushgateway         "/bin/pushgateway"       pushgateway         running             9091/tcp
[root@node01 stack]# 
```
#### Можно зайти по адресу ВМ и номеру порта и посмотреть запущенные сервисы

### Удаление ВМ
```bash
# В директории ./terraform выполнить
terraform destroy -auto-approve
```
