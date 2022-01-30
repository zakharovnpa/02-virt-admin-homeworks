# "6.2. SQL" - Захаров Сергей Николаевич

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.

**Ответ:**
## Создаем Volume для доступа данных из контейнера на локальную машину

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
### Запущенные контейнеры:
```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED        STATUS        PORTS                                       NAMES
d64c2e97d86a   postgres:12   "docker-entrypoint.s…"   13 hours ago   Up 13 hours   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   pg-netology
```
### Заходим в контейнер и запускаем в нем bash
```ps
root@server1:~# docker exec -it pg-netology bash
root@d64c2e97d86a:/# 
```
### Заходим в БД postgres как пользователь postgres
```ps
root@d64c2e97d86a:/# psql -U postgres
psql (12.9 (Debian 12.9-1.pgdg110+1))
Type "help" for help.

postgres=# 
```
### Проверяем права пользователя postgres

```ps
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=# 
postgres=# 

```
### Создаем БД test_db
```ps
postgres=# CREATE DATABASE test_db;
CREATE DATABASE
```
```ps
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(6 rows)
```

### Результат: инстанс запущен, БД в работе.

## Задача 2

В БД из задачи 1: 
- создайте пользователя test-admin-user и БД test_db
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
- создайте пользователя test-simple-user  
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db

Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:
- итоговый список БД после выполнения пунктов выше,
- описание таблиц (describe)
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
- список пользователей с правами над таблицами test_db

**Ответ:**

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
Входим в БД test_db
```ps
postgres=# \c test_db
You are now connected to database "test_db" as user "postgres".
```
Создаем таблицу orders
```ps
test_db=#  create table orders (id integer, name text, price integer, PRIMARY KEY (id));
CREATE TABLE
```
Создаем таблицу clients
```ps
test_db=# create table clients (id integer PRIMARY KEY, lastname text, country text, booking integer, FOREIGN KEY (booking) REFERENCES orders (Id));
CREATE TABLE
```
Таблицы orders и clients созданы
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


### Для ответа приведите:
- итоговый список БД после выполнения пунктов выше
```ps
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(6 rows)
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

## Задача 3

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы 
- приведите в ответе:
    - запросы 
    - результаты их выполнения.

**Ответ:**
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
  - запрос для наполнения данными таблицы orders
```ps
insert into orders VALUES (1, 'Шоколад', 10), (2, 'Принтер', 3000), (3, 'Книга', 500), (4, 'Монитор', 7000), (5, 'Гитара', 4000);

```
  - результат

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
  - запрос для наполнения данными таблицы clients
```ps
test_db=# insert into clients VALUES (1, 'Иванов Иван Иванович', 'USA'), (2, 'Петров Петр Петрович', 'Canada'), (3, 'Иоганн Себастьян Бах', 'Japan'), (4, 'Ронни Джеймс Дио', 'Russia'), (5, 'Ritchie Blackmore', 'Russia');
INSERT 0 5

```
  - результат

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
 запросы и результаты их выполнения
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

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:
```ps
|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |
```
Подсказка - используйте директиву `UPDATE`.

**Ответ:**
Приведите SQL-запросы для выполнения данных операций.
```ps
#Иванов Иван Иванович покупает книгу
test_db=# update  clients set booking = 3 where id = 1;
UPDATE 1

#Петров Петр Петрович покупает Монитор
test_db=# update  clients set booking = 4 where id = 2;
UPDATE 1

#Иоганн Себастьян Бах покупает Гитару
test_db=# update  clients set booking = 5 where id = 3;
UPDATE 1
```

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
```ps
test_db=# select * from clients as c where  exists (select id from orders as o where c.booking = o.id);
```
```ps
 id |       lastname       | country | booking 
----+----------------------+---------+---------
  1 | Иванов Иван Иванович | USA     |       3
  2 | Петров Петр Петрович | Canada  |       4
  3 | Иоганн Себастьян Бах | Japan   |       5
(3 rows)

```

## Задача 5


Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.

**Ответ:**

Выполняем запрос о покупках
 ```ps
test_db=# select * from clients as c where  exists (select id from orders as o where c.booking = o.id);
 id |       lastname       | country | booking 
----+----------------------+---------+---------
  1 | Иванов Иван Иванович | USA     |       3
  2 | Петров Петр Петрович | Canada  |       4
  3 | Иоганн Себастьян Бах | Japan   |       5
(3 rows)

```
Выполняем тот же запрос о покупках с использованием EXPLAIN
```ps
test_db=# explain select * from clients as c where  exists (select id from orders as o where c.booking = o.id);
                               QUERY PLAN                               
------------------------------------------------------------------------
 Hash Join  (cost=37.00..57.24 rows=810 width=72)
   Hash Cond: (c.booking = o.id)
   ->  Seq Scan on clients c  (cost=0.00..18.10 rows=810 width=72)
   ->  Hash  (cost=22.00..22.00 rows=1200 width=4)
         ->  Seq Scan on orders o  (cost=0.00..22.00 rows=1200 width=4)
(5 rows)

```
#### Пояснение:
Для оптимизации запросов очень важно понимать логику работы ядра PostgreSQL. EXPLAIN выводит информацию, необходимую для понимания, что же делает ядро при каждом конкретном запросе.

В нашем примере планировщик выбирает соединение по хешу (Hash Join), при котором строки одной таблицы записываются в хеш-таблицу в памяти, после чего сканируется другая таблица и для каждой её строки проверяется соответствие по хеш-таблице. Здесь отступы отражают структуру плана: результат сканирования битовой карты по clients подаётся на вход узлу Hash, который конструирует хеш-таблицу. Затем она передаётся узлу Hash Join, который читает строки из узла внешнего потомка и проверяет их по этой хеш-таблице.

1. Hash Join вызывает “Hash", который в свою очередь вызывает что-нибудь ещё (в нашем случае – Seq Scan по таблице orders). 
2. Потом Hash создает в памяти хэш/ассоциативный массив/словарь со строками из источника, хэшированными с помощью того, что используется для объединения данных (в нашем случае это столбец o.id в таблице clients).
3. Потом Hash Join запускает вторую субоперацию (Seq Scan по таблице clients в нашем случае) и, для каждой строки из неё, делает следующее:
  - Проверяет, есть ли ключ join (pg_class.relnamespace в данном случае) в хэше, возвращенном операцией Hash.
    - Если нет, данная строка из субоперации игнорируется (не будет возвращена).
    - Если ключ существует, Hash Join берет строки из хэша и, основываясь на этой строке, с одной стороны, и всех строках хэша, с другой стороны, генерирует вывод строк, что мы и получили на выходе.

#### Термины:
**Hash Join** - используется для объединения двух наборов записей.
**Hash Cond** - для каждой строки таблицы clients вычисляется hash, который сравнивается с hash таблицы orders по условию **Hash Cond**.  
**Sec Scan on clients c** - при выполнении запроса последовательно считывается каждая запись таблицы clients
**Hash** - для каждой строки orders вычисляется ее **Hash**.
**Seq Scan on orders o** - при выполнении запроса последовательно считывается каждая запись таблицы orders. 
**cost** — стоимость запроса в postgres story points. Это некое сферическое в вакууме понятие, призванное оценить затратность операции. Первое значение 0.00 — затраты на получение первой строки. Второе — 18.10 — затраты на получение всех строк.
**rows** — приблизительное количество возвращаемых строк при выполнении операции Seq Scan.
**width** — средний размер одной строки в байтах.

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

**Ответ:**

### Создаем бэкап БД test_db и помещаем его в volume, предназначенный для бэкапов (см. Задачу 1).
```ps
root@d64c2e97d86a:~# pg_dump -U postgres test_db -f /var/lib/postgresql/backup/dump_test_db.sql

```
Появление дампа БД в директории где лежит Volume
```ps
root@server1:/var/lib/docker/volumes/vol-2-pg-backup/_data# ls -l
total 4
-rw-r--r-- 1 root root 2439 Jan 29 09:26 dump_test_db.sql
```

Как найти директорию Volume
```ps
root@server1:~# docker volume inspect vol-2-pg-backup
[
    {
        "CreatedAt": "2022-01-26T04:28:35Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/vol-2-pg-backup/_data",
        "Name": "vol-2-pg-backup",
        "Options": {},
        "Scope": "local"
    }
]
root@server1:~# 
root@server1:~# 
root@server1:~# docker volume inspect vol-1-pg-base
[
    {
        "CreatedAt": "2022-01-29T06:37:00Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/vol-1-pg-base/_data",
        "Name": "vol-1-pg-base",
        "Options": {},
        "Scope": "local"
    }
]
root@server1:~# 
```

### Остановливаем контейнер с PostgreSQL (но не удаляйте volumes).
```ps
root@server1:~# docker container stop d64c2e97d86a
d64c2e97d86a
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@server1:~# 
```

### Поднимаем новый пустой контейнер с PostgreSQL.
```ps
root@server1:~# docker run -d --name pg-netology-2 -e POSTGRES_PASSWORD=postgres -p 5432:5432 -v vol-1-pg-base:/var/lib/postgresql/data -v vol-2-pg-backup:/var/lib/postgresql/backup postgres:12
pg-netology-2
```
Второй контейнер запустился
```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED              STATUS              PORTS                                       NAMES
84f3980f7c71   postgres:12   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   pg-netology-2
```

### Восстановливаем БД test_db в новом контейнере.
При создании нового контейнера pg-netology-2 волюмы подключились автоматически и БД считались также автоматически
```ps
root@server1:~# docker exec -it pg-netology-2 bash 
root@84f3980f7c71:/# 
root@84f3980f7c71:/# psql -U postgres
psql (12.9 (Debian 12.9-1.pgdg110+1))
Type "help" for help.


postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(6 rows)


```

### Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

Создание вручную бэкапа БД из shell контейнера docker
```ps
root@0eabb98f5d26:~# pg_dump -U postgres -d test_db -f /var/lib/postgresql/dump_test_db_1.sql
root@0eabb98f5d26:~# 
```
```ps
root@0eabb98f5d26:/var/lib/postgresql# 
root@0eabb98f5d26:/var/lib/postgresql# ls -l
total 12
drwxr-xr-x  2 root     root     4096 Jan 29 09:26 backup
drwx------ 19 postgres postgres 4096 Jan 30 04:56 data
-rw-r--r--  1 root     root     2220 Jan 30 07:06 dump_test_db_1.sql
```
Удаляем БД test_db
```ps
postgres=# drop database test_db:
DROP DATABASE
```
Перед восстановлением из бэкапа создаем заново пустую БД с тем же именем test_db:
```ps
postgres=# create database test_db;
CREATE DATABASE
```
Выходим из СУБД в shell контейнера:
```ps
postgres=# \q
```
Восстанавливаем БД test_db из бэкапа:
```ps
root@0eabb98f5d26:~# psql -U postgres -d test_db -f /var/lib/postgresql/dump_test_db_2.sql
SET
SET
SET
SET
SET
 set_config 
------------
 
(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
COPY 3
COPY 5
ALTER TABLE
ALTER TABLE
ALTER TABLE
GRANT
GRANT
root@0eabb98f5d26:~# 

```
Подкллючаемся к СУБД
```ps
root@0eabb98f5d26:~# psql -U postgres
psql (12.9 (Debian 12.9-1.pgdg110+1))
Type "help" for help.
```
БД test_db появилась в списке доступных баз данных
```ps
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(5 rows)

```
Подключаемся к БД
```ps
postgres=# \c test_db
You are now connected to database "test_db" as user "postgres".
```
Доступные таблицы
```ps
test_db=# \dt
          List of relations
 Schema |  Name   | Type  |  Owner   
--------+---------+-------+----------
 public | clients | table | postgres
 public | orders  | table | postgres
(2 rows)
```
Доступные данные в таблицах
```ps
test_db=# select * from clients;
 id |       lastname       | country | booking 
----+----------------------+---------+---------
  1 | Иванов Иван Иванович | USA     |        
  3 | Иоганн Себастьян Бах | Japan   |        
  5 | Ritchie Blackmore    | Russia  |        
(3 rows)

test_db=# 
test_db=# select * from orders;
 id |  name   | price 
----+---------+-------
  1 | Шоколад |    10
  2 | Принтер |  3000
  3 | Книга   |   500
  4 | Монитор |  7000
  5 | Гитара  |  4000
(5 rows)

```
Задание выполнено: при создании нового контейнера из волюма БД автоматически подключилась. А при создании бэкапа вручную, также вручную БД восстановилась.

---

