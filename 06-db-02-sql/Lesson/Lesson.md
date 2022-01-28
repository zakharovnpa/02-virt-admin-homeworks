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
Установка приложения dbeaver
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
Запущенные контейнеры:
```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED        STATUS        PORTS                                       NAMES
d64c2e97d86a   postgres:12   "docker-entrypoint.s…"   13 hours ago   Up 13 hours   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   pg-netology
root@server1:~# 
root@server1:~# 
```
Просмотр ip адреса ВМ с Докером:
```ps
root@server1:~# ip add
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:73:60:cf brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 76813sec preferred_lft 76813sec
    inet6 fe80::a00:27ff:fe73:60cf/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:49:28:c2 brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.11/24 brd 192.168.56.255 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe49:28c2/64 scope link 
       valid_lft forever preferred_lft forever
4: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:c7:c9:6e:44 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:c7ff:fec9:6e44/64 scope link 
       valid_lft forever preferred_lft forever
6: vetha51279b@if5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default 
    link/ether 0a:50:34:3d:89:8a brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::850:34ff:fe3d:898a/64 scope link 
       valid_lft forever preferred_lft forever
root@server1:~# 
root@server1:~# 
```
```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED        STATUS        PORTS                                       NAMES
d64c2e97d86a   postgres:12   "docker-entrypoint.s…"   13 hours ago   Up 13 hours   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   pg-netology
root@server1:~# 
```
Заходим в контейнер и запускаем в нем bash
```ps
root@server1:~# docker exec -it pg-netology bash
root@d64c2e97d86a:/# 
root@d64c2e97d86a:/# ls -alh
total 84K
drwxr-xr-x   1 root root 4.0K Jan 26 05:29 .
drwxr-xr-x   1 root root 4.0K Jan 26 05:29 ..
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 bin
drwxr-xr-x   2 root root 4.0K Dec 11 17:25 boot
drwxr-xr-x   5 root root  360 Jan 26 05:29 dev
drwxr-xr-x   2 root root 4.0K Dec 21 23:32 docker-entrypoint-initdb.d
-rwxr-xr-x   1 root root    0 Jan 26 05:29 .dockerenv
drwxr-xr-x   1 root root 4.0K Jan 26 05:29 etc
drwxr-xr-x   2 root root 4.0K Dec 11 17:25 home
drwxr-xr-x   1 root root 4.0K Dec 20 00:00 lib
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 lib64
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 media
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 mnt
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 opt
dr-xr-xr-x 170 root root    0 Jan 26 05:29 proc
drwx------   1 root root 4.0K Dec 21 23:31 root
drwxr-xr-x   1 root root 4.0K Dec 21 23:33 run
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 sbin
drwxr-xr-x   2 root root 4.0K Dec 20 00:00 srv
dr-xr-xr-x  13 root root    0 Jan 26 05:29 sys
drwxrwxrwt   1 root root 4.0K Dec 21 23:34 tmp
drwxr-xr-x   1 root root 4.0K Dec 20 00:00 usr
drwxr-xr-x   1 root root 4.0K Dec 20 00:00 var
root@d64c2e97d86a:/# 
root@d64c2e97d86a:/# 
```
Запускаем команду
```ps
root@d64c2e97d86a:/# psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "root" does not exist
root@d64c2e97d86a:/# 
root@d64c2e97d86a:/# 
```
Заходим в БД postgres как пользователь postgres
```ps
root@d64c2e97d86a:/# psql -U postgres
psql (12.9 (Debian 12.9-1.pgdg110+1))
Type "help" for help.

postgres=# 
```
Проверяем пава пользователя postgres

```ps
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=# 
postgres=# 

```
Результат: инстанс запущен, БД в работе.

## Ход выполнения Задания №2

В БД из задачи 1: 
### 1 - создайте пользователя test-admin-user и БД test_db

```ps
postgres=# CREATE ROLE "test-admin-user" SUPERUSER NOCREATEDB NOCREATEROLE NOINHERIT LOGIN;
CREATE ROLE
```
Видим появление нового пользователя
```ps
postgres=# \du
                                      List of roles
    Role name    |                         Attributes                         | Member of 
-----------------+------------------------------------------------------------+-----------
 postgres        | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 test-admin-user | Superuser, No inheritance                                  | {}

postgres=# 
```
### 2 - в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
```ps
Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)
```
Входим в БД test_db и создаем таблицу orders
```ps
postgres=# \c test_db
You are now connected to database "test_db" as user "postgres".
```
```ps
test_db=#  create table orders (id integer, name text, price integer, PRIMARY KEY (id));
CREATE TABLE
```
Таблица orders создана
```ps
test_db=#  \dt
         List of relations
 Schema |  Name  | Type  |  Owner   
--------+--------+-------+----------
 public | orders | table | postgres
(1 row)

```
Создаем таблицу clients
```ps
test_db=# create table clients (id integer PRIMARY KEY, lastname text, country text, booking integer, FOREIGN KEY (booking) REFERENCES orders (Id));
CREATE TABLE
```
Таблица clients создана
```ps
test_db=# \dt
          List of relations
 Schema |  Name   | Type  |  Owner   
--------+---------+-------+----------
 public | clients | table | postgres
 public | orders  | table | postgres
(2 rows)

```

### 3 - предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
```ps
test_db=# grant all on public.orders to "test-admin-user";
GRANT
test_db=# 
test_db=# grant all on public.clients to "test-admin-user";
GRANT

```

### 4 - создайте пользователя test-simple-user  
Создание пользователя test-simple-user
```ps
test_db=# create role "test-simple-user" nosuperuser nocreatedb nocreaterole noinherit login; 
CREATE ROLE

```
Новый пользователь в списке
```ps
test_db=# \du
                                       List of roles
    Role name     |                         Attributes                         | Member of 
------------------+------------------------------------------------------------+-----------
 postgres         | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 test-admin-user  | Superuser, No inheritance                                  | {}
 test-simple-user | No inheritance   

```

### 5 - предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db
```ps
test_db=# grant select on table public.clients to "test-simple-user";
GRANT
test_db=# grant insert on table public.clients to "test-simple-user";
GRANT
test_db=# grant update on table public.clients to "test-simple-user";
GRANT
test_db=# grant delete on table public.clients to "test-simple-user";
GRANT
test_db=# 
test_db=# grant select on table public.orders to "test-simple-user";
GRANT
test_db=# grant insert on table public.orders to "test-simple-user";
GRANT
test_db=# grant update on table public.orders to "test-simple-user";
GRANT
test_db=# grant delete on table public.orders to "test-simple-user";
GRANT

```


### Приведите:
- итоговый список БД после выполнения пунктов выше,
```ps
test_db=# \du
                                       List of roles
    Role name     |                         Attributes                         | Member of 
------------------+------------------------------------------------------------+-----------
 postgres         | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 test-admin-user  | Superuser, No inheritance                                  | {}
 test-simple-user | No inheritance                                             | {}
```
- описание таблиц (describe)
```ps
test_db=# \dt
          List of relations
 Schema |  Name   | Type  |  Owner   
--------+---------+-------+----------
 public | clients | table | postgres
 public | orders  | table | postgres
(2 rows)
```

- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
```ps
select * from INFORMATION_SCHEMA.TABLE_PRIVILEGES where grantee in ('test-admin-user', 'test-simple-user');
```
- список пользователей с правами над таблицами test_db
```ps
test_db=# select * from INFORMATION_SCHEMA.TABLE_PRIVILEGES where grantee in ('test-admin-user', 'test-simple-user');
 grantor  |     grantee      | table_catalog | table_schema | table_name | privilege_type | is_grantable | with_hierarchy 
----------+------------------+---------------+--------------+------------+----------------+--------------+----------------
 postgres | test-simple-user | test_db       | public       | orders     | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | orders     | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | DELETE         | NO           | NO
 postgres | test-admin-user  | test_db       | public       | orders     | INSERT         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | orders     | SELECT         | YES          | YES
 postgres | test-admin-user  | test_db       | public       | orders     | UPDATE         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | orders     | DELETE         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | orders     | TRUNCATE       | YES          | NO
 postgres | test-admin-user  | test_db       | public       | orders     | REFERENCES     | YES          | NO
 postgres | test-admin-user  | test_db       | public       | orders     | TRIGGER        | YES          | NO
 postgres | test-simple-user | test_db       | public       | clients    | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | clients    | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | DELETE         | NO           | NO
 postgres | test-admin-user  | test_db       | public       | clients    | INSERT         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | clients    | SELECT         | YES          | YES
 postgres | test-admin-user  | test_db       | public       | clients    | UPDATE         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | clients    | DELETE         | YES          | NO
 postgres | test-admin-user  | test_db       | public       | clients    | TRUNCATE       | YES          | NO
 postgres | test-admin-user  | test_db       | public       | clients    | REFERENCES     | YES          | NO
 postgres | test-admin-user  | test_db       | public       | clients    | TRIGGER        | YES          | NO
(22 rows)
```

## Ход выполнения Задания №3

#### 1- Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:
```ps
Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|
```
```ps
Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|
```

Состояние таблиц до внесения данных
```ps
test_db=# select * from clients;
 id | lastname | country | booking 
----+----------+---------+---------
(0 rows)

test_db=# 
test_db=# select * from orders;
 id | name | price 
----+------+-------
(0 rows)

test_db=# 
test_db=# select count (*) from clients;
 count 
-------
     0
(1 row)

test_db=# 
test_db=# select count (*) from orders;
 count 
-------
     0
(1 row)

```
  - запросы для наполнения данными таблицы orders
```ps
insert into orders VALUES (1, 'Шоколад', 10), (2, 'Принтер', 3000), (3, 'Книга', 500), (4, 'Монитор', 7000), (5, 'Гитара', 4000);

```
  - результаты их выполнения.

```ps
test_db=# select * from orders;
 id |  name   | price 
----+---------+-------
  1 | Шоколад |    10
  2 | Принтер |  3000
  3 | Книга   |   500
  4 | Монитор |  7000
  5 | Гитара  |  4000
(5 rows)

test_db=# 
```
  - запросы для наполнения данными таблицы clients
```ps
test_db=# insert into clients VALUES (1, 'Иванов Иван Иванович', 'USA'), (2, 'Петров Петр Петрович', 'Canada'), (3, 'Иоганн Себастьян Бах', 'Japan'), (4, 'Ронни Джеймс Дио', 'Russia'), (5, 'Ritchie Blackmore', 'Russia');
INSERT 0 5

```
  - результаты их выполнения.

```ps
test_db=# select * from clients;
 id |       lastname       | country | booking 
----+----------------------+---------+---------
  1 | Иванов Иван Иванович | USA     |        
  2 | Петров Петр Петрович | Canada  |        
  3 | Иоганн Себастьян Бах | Japan   |        
  4 | Ронни Джеймс Дио     | Russia  |        
  5 | Ritchie Blackmore    | Russia  |        
(5 rows)

```

#### 2 - Используя SQL синтаксис вычислите количество записей для каждой таблицы 

- приведите в ответе:
    - запросы 
    - результаты их выполнения.

```ps
test_db=# select count (*) from orders;
 count 
-------
     5
(1 row)
```

```ps
test_db=# select count (*) from clients;
 count 
-------
     5
(1 row)
```
## Ход выполнения Задания №4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения данных операций.
```ps
test_db=# update  clients set booking = 3 where id = 1;         #Иванов Иван Иванович покупает Книгу
UPDATE 1

test_db=# update  clients set booking = 4 where id = 2;         #Петров Петр Петрович покупает Монитор 
UPDATE 1

test_db=# update  clients set booking = 5 where id = 3;         #Иоганн Себастьян Бах покупает Гитару
UPDATE 1
```

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
 ```ps
test_db=# select * from clients as c where  exists (select id from orders as o where c.booking = o.id);
 id |       lastname       | country | booking 
----+----------------------+---------+---------
  1 | Иванов Иван Иванович | USA     |       3
  2 | Петров Петр Петрович | Canada  |       4
  3 | Иоганн Себастьян Бах | Japan   |       5
(3 rows)

 ```
Подсказк - используйте директиву `UPDATE`.
