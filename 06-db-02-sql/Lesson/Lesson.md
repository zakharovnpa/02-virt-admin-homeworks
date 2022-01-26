## Ход выполнения Задания №1

Используя docker:
* поднимите инстанс PostgreSQL (версию 12)
* с 2 volume
* в volume будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.

### Поиск ` PostgreSQL ` образа на Docker-hub

```ps
root@server1:~# docker search PostgreSQL
NAME                                         DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
postgres                                     The PostgreSQL object-relational database sy…   10489     [OK]       
sameersbn/postgresql                                                                         161                  [OK]
paintedfox/postgresql                        A docker image for running Postgresql.          77                   [OK]
orchardup/postgresql                         https://github.com/orchardup/docker-postgres…   49                   [OK]
centos/postgresql-96-centos7                 PostgreSQL is an advanced Object-Relational …   45                   
jbergknoff/postgresql-client                                                                 20                   [OK]
centos/postgresql-10-centos7                 PostgreSQL is an advanced Object-Relational …   19                   
centos/postgresql-94-centos7                 PostgreSQL is an advanced Object-Relational …   16                   
xcgd/postgresql                              The PostgreSQL object-relational database sy…   11                   [OK]
ckan/postgresql                              PostgreSQL image for CKAN                       8                    [OK]
centos/postgresql-95-centos7                 PostgreSQL is an advanced Object-Relational …   6                    
tozd/postgresql                              PostgreSQL Docker image.                        5                    [OK]
centos/postgresql-12-centos7                 PostgreSQL is an advanced Object-Relational …   4                    
frodenas/postgresql                          A Docker Image for PostgreSQL                   4                    [OK]
ansibleplaybookbundle/postgresql-apb         An APB which deploys RHSCL PostgreSQL           2                    [OK]
tmaier/postgresql-client                     Run the PostgreSQL Client (psql) within a do…   2                    [OK]
postgresqlaasdockerhub/docker-postgresql94   docker hub build for postgresql 94              2                    [OK]
postgresqlaasdockerhub/docker-postgresql96   docker hub build for postgresql 96              1                    [OK]
openshift/postgresql-92-centos7              DEPRECATED: A Centos7 based PostgreSQL v9.2 …   1                    
nanobox/postgresql                           Postgresql service for nanobox.io               1                    [OK]
manageiq/postgresql                          Container with PostgreSQL and built on CentO…   0                    [OK]
cfcommunity/postgresql-base                  https://github.com/cloudfoundry-community/po…   0                    
cfcommunity/postgresql                       https://github.com/cloudfoundry-community/po…   0                    
tommy351/postgresql-client                   PostgreSQL client                               0                    [OK]
oriaks/postgresql  

```
Выбираем образ ` postgres ` (с наибольшим количеством звезд)

Но нам необходимо найти postgres версии 12:
```ps
root@server1:~# docker search postgres | grep 12
centos/postgresql-12-centos7            PostgreSQL is an advanced Object-Relational …   4 
```
Или:
```ps
root@server1:~# docker search postgres:12
NAME                                                DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
breezuh/postgres-non-durable                        Runs postgres:12-alpine in non-durable mode     0                    
teikadev/postgres12-partman                         postgres:12.1-alpine with pg_partman 4.2.2 i…   0                    
olback/postgres12-pg-cron                           postgres:12-alpine with pg_cron                 0                    
jomarquez/postgres12-pgtap                          Installs pgtap and pg-prove on postgres:12.4…   0                    
jaredreisinger/postgres-12beta3-alpine-hashids      A variant of postgres:12-beta3-alpine, with …   0                    
arturhg/multi-postgres                              A docker image based on postgres:12-alpine t…   0                    
ankitjaiinn/postgres-postgis-gdal-python            It has postgres:12-alpine, postgis3, python3    0                    
christianhohlfeld/postgres                          postgres:12.2                                   0                    
jaredreisinger/postgres-12beta3-alpine-dev          A variant of the postgres:12-beta3-alpine im…   0                    
stevebunlon/fa-blog-ts-postgres                     Postgres:12.5 database for the lumber typesc…   0                    
jaredreisinger/postgres-12beta3-alpine-ap_pgutils   A variant of postgres:12-beta3-alpine, with …   0 
```
### Создаем Volume для доступа данных из контейнера на локальную машину

```ps
root@server1:~# docker volume create vol-1-pg-base
vol-1-pg-base
root@server1:~# 
root@server1:~# docker volume create vol-2-pg-backup
vol-2-pg-backup
```
```ps
root@server1:~# docker volume ls
DRIVER    VOLUME NAME
local     vol-1-pg-base
local     vol-2-pg-backup

```
Скачиваем образ
```ps
root@server1:~# docker pull postgres:12
12: Pulling from library/postgres
a2abf6c4d29d: Pull complete 
e1769f49f910: Pull complete 
33a59cfee47c: Pull complete 
461b2090c345: Pull complete 
8ed8ab6290ac: Pull complete 
495e42c822a0: Pull complete 
18e858c71c58: Pull complete 
594792c80d5f: Pull complete 
0cc21527d805: Pull complete 
c33105c93a6d: Pull complete 
f0d44539f7e1: Pull complete 
2237b54399af: Pull complete 
59525896cd85: Pull complete 
Digest: sha256:1d098cd3c1a7b132edc5bfdd7d775ff0949104b150e31d52c0aff7bdcd25c53e
Status: Downloaded newer image for postgres:12
docker.io/library/postgres:12
```

```ps
root@server1:~# docker image ls
REPOSITORY                    TAG        IMAGE ID       CREATED         SIZE
postgres                      12         58bff7631346   3 weeks ago     371MB

```
Пример скачивания другого образа:

```ps
root@server1:~# docker pull teikadev/postgres12-partman
Using default tag: latest
latest: Pulling from teikadev/postgres12-partman
4167d3e14976: Pull complete 
153ce209e2ba: Pull complete 
b5e6278dc07d: Pull complete 
aa4e6681b786: Pull complete 
9a46c001bf9b: Pull complete 
1df507bf92bc: Pull complete 
f42c81d5a6e1: Pull complete 
d92b9ec99c87: Pull complete 
7977fcd6ee85: Pull complete 
Digest: sha256:ac155369eace484d8967f2cb6eb691cb32dd9102f3f968ed23a4abf549acfc88
Status: Downloaded newer image for teikadev/postgres12-partman:latest
docker.io/teikadev/postgres12-partman:latest
```
```ps
root@server1:~# docker image ls
REPOSITORY                    TAG        IMAGE ID       CREATED         SIZE
teikadev/postgres12-partman   latest     63db8bbf0186   23 months ago   155MB

```
### Поднимаем инстанс
```ps
root@server1:~# docker run -it --name pg-netology -e POSTGRES_PASSWORD=postgres -p 5432:5432 -v vol-1-pg-base:/var/lib/postgresql/data -v vol-2-pg-backup:/var/lib/postgresql/backup postgres:12
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.utf8".
The default database encoding has accordingly been set to "UTF8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgresql/data ... ok
creating subdirectories ... ok
selecting dynamic shared memory implementation ... posix
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting default time zone ... Etc/UTC
creating configuration files ... ok
running bootstrap script ... ok
performing post-bootstrap initialization ... ok
syncing data to disk ... ok

initdb: warning: enabling "trust" authentication for local connections
You can change this by editing pg_hba.conf or using the option -A, or
--auth-local and --auth-host, the next time you run initdb.

Success. You can now start the database server using:

    pg_ctl -D /var/lib/postgresql/data -l logfile start

waiting for server to start....2022-01-26 05:29:56.347 UTC [47] LOG:  starting PostgreSQL 12.9 (Debian 12.9-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
2022-01-26 05:29:56.350 UTC [47] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2022-01-26 05:29:56.382 UTC [48] LOG:  database system was shut down at 2022-01-26 05:29:55 UTC
2022-01-26 05:29:56.390 UTC [47] LOG:  database system is ready to accept connections
 done
server started

/usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*

2022-01-26 05:29:56.584 UTC [47] LOG:  received fast shutdown request
waiting for server to shut down....2022-01-26 05:29:56.589 UTC [47] LOG:  aborting any active transactions
2022-01-26 05:29:56.596 UTC [47] LOG:  background worker "logical replication launcher" (PID 54) exited with exit code 1
2022-01-26 05:29:56.597 UTC [49] LOG:  shutting down
2022-01-26 05:29:56.616 UTC [47] LOG:  database system is shut down
 done
server stopped

PostgreSQL init process complete; ready for start up.

2022-01-26 05:29:56.706 UTC [1] LOG:  starting PostgreSQL 12.9 (Debian 12.9-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
2022-01-26 05:29:56.708 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
2022-01-26 05:29:56.710 UTC [1] LOG:  listening on IPv6 address "::", port 5432
2022-01-26 05:29:56.714 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2022-01-26 05:29:56.735 UTC [66] LOG:  database system was shut down at 2022-01-26 05:29:56 UTC
2022-01-26 05:29:56.741 UTC [1] LOG:  database system is ready to accept connections

```
```ps
maestro@PC-Ubuntu:~/Рабочий стол$ sudo apt install dbeaver-community
[sudo] пароль для maestro: 
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
E: Невозможно найти пакет dbeaver-community
maestro@PC-Ubuntu:~/Рабочий стол$ 
maestro@PC-Ubuntu:~/Рабочий стол$ 
maestro@PC-Ubuntu:~/Рабочий стол$ sudo snap install dbeaver-ce
dbeaver-ce 21.3.3.202201221033 от DBeaver (dbeaver-corp) установлен
maestro@PC-Ubuntu:~/Рабочий стол$ 
maestro@PC-Ubuntu:~/Рабочий стол$ 

```
