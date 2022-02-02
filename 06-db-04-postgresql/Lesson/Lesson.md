## Ход выполнения ДЗ по теме "PostgresSQL"

### Ход выполнения Задания №1


#### Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

```ps
root@server1:~# docker volume create pg_backup
pg_backup

```

```ps
root@server1:~# docker run -it --name pg-sql-netology -e POSTGRES_PASSWORD=postgres -p 5432:4532 -v pg_backup:/var/lib/postgresql/data postgres:13
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

waiting for server to start....2022-02-01 18:26:59.118 UTC [47] LOG:  starting PostgreSQL 13.5 (Debian 13.5-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
2022-02-01 18:26:59.122 UTC [47] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2022-02-01 18:26:59.135 UTC [48] LOG:  database system was shut down at 2022-02-01 18:26:58 UTC
2022-02-01 18:26:59.141 UTC [47] LOG:  database system is ready to accept connections
 done
server started

/usr/local/bin/docker-entrypoint.sh: ignoring /docker-entrypoint-initdb.d/*

2022-02-01 18:26:59.340 UTC [47] LOG:  received fast shutdown request
waiting for server to shut down....2022-02-01 18:26:59.344 UTC [47] LOG:  aborting any active transactions
2022-02-01 18:26:59.348 UTC [47] LOG:  background worker "logical replication launcher" (PID 54) exited with exit code 1
2022-02-01 18:26:59.350 UTC [49] LOG:  shutting down
2022-02-01 18:26:59.366 UTC [47] LOG:  database system is shut down
 done
server stopped

PostgreSQL init process complete; ready for start up.

2022-02-01 18:26:59.481 UTC [1] LOG:  starting PostgreSQL 13.5 (Debian 13.5-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
2022-02-01 18:26:59.483 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
2022-02-01 18:26:59.484 UTC [1] LOG:  listening on IPv6 address "::", port 5432
2022-02-01 18:26:59.489 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2022-02-01 18:26:59.495 UTC [59] LOG:  database system was shut down at 2022-02-01 18:26:59 UTC
2022-02-01 18:26:59.502 UTC [1] LOG:  database system is ready to accept connections

```

#### Подключитесь к БД PostgreSQL используя `psql`.
```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                                                 NAMES
49db9913bea2   postgres:13   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   5432/tcp, 0.0.0.0:5432->4532/tcp, :::5432->4532/tcp   pg-sql-netology
root@server1:~# 
root@server1:~# docker exec -t pg-sql-netology bash
root@49db9913bea2:/# 

```
Подключаемся к терминалу в контейнере
```ps
root@server1:~# docker exec -it pg-sql-netology bash
root@49db9913bea2:/# 
```
Подключаемся к БД
```ps
root@49db9913bea2:/# psql
psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  role "root" does not exist
root@49db9913bea2:/# 
root@49db9913bea2:/# psql -U postgres
psql (13.5 (Debian 13.5-1.pgdg110+1))
Type "help" for help.

postgres=# 
postgres=# 
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)

postgres=# 
postgres=# 
```

#### Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.
```ps
root@49db9913bea2:/# psql -?
psql is the PostgreSQL interactive terminal.

Usage:
  psql [OPTION]... [DBNAME [USERNAME]]

General options:
  -c, --command=COMMAND    run only single command (SQL or internal) and exit
  -d, --dbname=DBNAME      database name to connect to (default: "root")
  -f, --file=FILENAME      execute commands from file, then exit
  -l, --list               list available databases, then exit
  -v, --set=, --variable=NAME=VALUE
                           set psql variable NAME to VALUE
                           (e.g., -v ON_ERROR_STOP=1)
  -V, --version            output version information, then exit
  -X, --no-psqlrc          do not read startup file (~/.psqlrc)
  -1 ("one"), --single-transaction
                           execute as a single transaction (if non-interactive)
  -?, --help[=options]     show this help, then exit
      --help=commands      list backslash commands, then exit
      --help=variables     list special variables, then exit

Input and output options:
  -a, --echo-all           echo all input from script
  -b, --echo-errors        echo failed commands
  -e, --echo-queries       echo commands sent to server
  -E, --echo-hidden        display queries that internal commands generate
  -L, --log-file=FILENAME  send session log to file
  -n, --no-readline        disable enhanced command line editing (readline)
  -o, --output=FILENAME    send query results to file (or |pipe)
  -q, --quiet              run quietly (no messages, only query output)
  -s, --single-step        single-step mode (confirm each query)
  -S, --single-line        single-line mode (end of line terminates SQL command)

Output format options:
  -A, --no-align           unaligned table output mode
      --csv                CSV (Comma-Separated Values) table output mode
  -F, --field-separator=STRING
                           field separator for unaligned output (default: "|")
  -H, --html               HTML table output mode
  -P, --pset=VAR[=ARG]     set printing option VAR to ARG (see \pset command)
  -R, --record-separator=STRING
                           record separator for unaligned output (default: newline)
  -t, --tuples-only        print rows only
  -T, --table-attr=TEXT    set HTML table tag attributes (e.g., width, border)
  -x, --expanded           turn on expanded table output
  -z, --field-separator-zero
                           set field separator for unaligned output to zero byte
  -0, --record-separator-zero
                           set record separator for unaligned output to zero byte

Connection options:
  -h, --host=HOSTNAME      database server host or socket directory (default: "local socket")
  -p, --port=PORT          database server port (default: "5432")
  -U, --username=USERNAME  database user name (default: "root")
  -w, --no-password        never prompt for password
  -W, --password           force password prompt (should happen automatically)

For more information, type "\?" (for internal commands) or "\help" (for SQL
commands) from within psql, or consult the psql section in the PostgreSQL
documentation.

Report bugs to <pgsql-bugs@lists.postgresql.org>.
PostgreSQL home page: <https://www.postgresql.org/>


```

#### **Найдите и приведите** управляющие команды для:
- вывода списка БД
```ps
root@49db9913bea2:/# psql -l -U postgres
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
(3 rows)

```
- подключения к БД
```ps
root@49db9913bea2:/# psql -U postgres test_db
psql (13.5 (Debian 13.5-1.pgdg110+1))
Type "help" for help.

test_db=# 
test_db=# 
```
- вывода списка таблиц
```ps
root@49db9913bea2:/# psql -c '\dt' -U postgres test_db
         List of relations
 Schema |  Name  | Type  |  Owner   
--------+--------+-------+----------
 public | orders | table | postgres
(1 row)

```

- вывода описания содержимого таблиц
```ps
root@49db9913bea2:/# psql -U postgres test_db -c 'select * from orders'
 id |  name   | price 
----+---------+-------
  1 | Шоколад |    10
  2 | Принтер |  3000
  3 | Книга   |   500
  4 | Монитор |  7000
  5 | Гитара  |  4000
(5 rows)

```
- выхода из psql
```ps
test_db=# \q
root@49db9913bea2:/# 

```
### 

## Задача 2
### Ход выполнения Задания №2

Используя `psql` создайте БД `test_database`.

```ps
root@49db9913bea2:/# psql -U postgres test_db -c 'create database test_database'
CREATE DATABASE
root@49db9913bea2:/# 
```
```ps
root@49db9913bea2:/# psql -c '\l' -U postgres
                                   List of databases
     Name      |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
---------------+----------+----------+------------+------------+-----------------------
 postgres      | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
               |          |          |            |            | postgres=CTc/postgres
 template1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
               |          |          |            |            | postgres=CTc/postgres
 test_database | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 test_db       | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
(5 rows)

```

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).


Восстановите бэкап БД в `test_database`.
```ps
root@49db9913bea2:~# psql -U postgres -f /var/lib/postgresql/data/test_database.sql test_database
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
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 8
 setval 
--------
      8
(1 row)

ALTER TABLE
root@49db9913bea2:~# 

```

Перейдите в управляющую консоль `psql` внутри контейнера.
```ps
root@49db9913bea2:~# psql -U postgres
psql (13.5 (Debian 13.5-1.pgdg110+1))
Type "help" for help.

postgres=# 

```

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.
```ps
postgres=# \c test_database
You are now connected to database "test_database" as user "postgres".
test_database=# 
```

```ps
test_database=# \dt
         List of relations
 Schema |  Name  | Type  |  Owner   
--------+--------+-------+----------
 public | orders | table | postgres
(1 row)

```

```ps
test_database=# ANALYZE VERBOSE public.orders;
INFO:  analyzing "public.orders"
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
ANALYZE
```

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.
```ps
test_database=# select avg_width from pg_stats where tablename='orders';
 avg_width 
-----------
         4
        16
         4
(3 rows)

```

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

**Ответ:**
```ps
select avg_width from pg_stats where tablename='orders';
```


## Задача 3
### Ход выполнения Задания №3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

**Ответ:**

Преобразовать обычную таблицу в секционированную и наоборот нельзя. Однако в секционированную таблицу можно добавить в качестве секции существующую обычную или секционированную таблицу, а также можно удалить секцию из секционированной таблицы и превратить её в отдельную таблицу; это может ускорить многие процессы обслуживания.
В нашем случае нет возможности для преобразование таблицы ` orders ` из обычной в секционированную.
#### Для решения задачи применим метод переноса данных в новую, уже секционированную таблицу.

Сохраняем таблицу ` orders ` под другим именем: ` orders_copy `
```ps
test_database=# alter table orders rename to orders_copy;
ALTER TABLE
test_database=# 
test_database=# 
test_database=# \dt
            List of relations
 Schema |    Name     | Type  |  Owner   
--------+-------------+-------+----------
 public | orders_copy | table | postgres
(1 row)

```
Создаем новую таблицу ` orders `, уже секционированную (Type - partitioned table). Граница секции будет по столбцу ` price `: 
```ps
test_database=# create table orders (id integer, title varchar(80), price integer) partition by range(price);
CREATE TABLE
test_database=# 
test_database=# \dt
                  List of relations
 Schema |    Name     |       Type        |  Owner   
--------+-------------+-------------------+----------
 public | orders      | partitioned table | postgres
 public | orders_copy | table             | postgres
(2 rows)

```
А теперь приступаем к разделению (шардированию) таблицы ` orders ` на две отдельные таблицы по условию: 
- в таблице ` peice_2 ` будет стоимость менее или рвено 499:
```ps
test_database=# create table orders_2 partition of orders for values from (0) to (500);
CREATE TABLE
test_database=# 
test_database=# \dt
                   List of relations
 Schema |      Name      |       Type        |  Owner   
--------+----------------+-------------------+----------
 public | orders         | partitioned table | postgres
 public | orders_copy    | table             | postgres
 public | orders_2       | table             | postgres
(3 rows)

```
А в таблице ` orders_1 ` будет стоимость от 500 и выше:
```ps
test_database=# create table orders_1 partition of orders for values from (500) to (1000);
CREATE TABLE
test_database=# \dt
                   List of relations
 Schema |      Name      |       Type        |  Owner   
--------+----------------+-------------------+----------
 public | orders         | partitioned table | postgres
 public | orders_copy    | table             | postgres
 public | orders_2       | table             | postgres
 public | orders_1       | table             | postgres
(4 rows)

```
Переносим данные из копии первоначальной таблицы ` orders_copy ` в  новую таблицу ` orders `:
```ps
test_database=# insert into orders (id, title, price) select * from orders_copy;
INSERT 0 8
test_database=# 
```
Получившиеся таблиы:
```ps
test_database=# \dt
                   List of relations
 Schema |      Name      |       Type        |  Owner   
--------+----------------+-------------------+----------
 public | orders         | partitioned table | postgres
 public | orders_copy    | table             | postgres
 public | orders_2       | table             | postgres
 public | orders_1       | table             | postgres
(4 rows)

```
Эти две новые таблицы пустые
```ps
test_database=# select * from orders_1;
 id | title | price 
----+-------+-------
(0 rows)

```
Выполним копирование данных в таблицу ` orders ` из сохраненной копии данных в таблице ` orders_copy `
```ps
test_database=# insert into orders (id, title, price) select * from orders_copy;
INSERT 0 8

```

#### Результаты выполненных запросов:
```ps
test_database=# select * from orders;
 id |        title         | price 
----+----------------------+-------
  1 | War and peace        |   100
  3 | Adventure psql time  |   300
  4 | Server gravity falls |   300
  5 | Log gossips          |   123
  2 | My little database   |   500
  6 | WAL never lies       |   900
  7 | Me and my bash-pet   |   499
  8 | Dbiezdmin            |   501
(8 rows)
```

```ps
test_database=# select * from orders_1;
 id |       title        | price 
----+--------------------+-------
  2 | My little database |   500
  6 | WAL never lies     |   900
  8 | Dbiezdmin          |   501
(3 rows)

```

```ps
test_database=# select * from orders_2;
 id |        title         | price 
----+----------------------+-------
  1 | War and peace        |   100
  3 | Adventure psql time  |   300
  4 | Server gravity falls |   300
  5 | Log gossips          |   123
  7 | Me and my bash-pet   |   499
(5 rows)

```

## Задача 4
### Ход выполнения Задания №4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

**Ответ:**
```ps

```
