## Ход выполнения ДЗ по теме "PostgresSQL"

Ссылки из лекции:
* [1-Популярные расширения для PostgreSQL: как установить и для чего использовать ](https://selectel.ru/blog/extensions/)
* [2- CREATE EXTENSION — установить расширение](https://postgrespro.ru/docs/postgresql/9.6/sql-createextension)
* [3-PgBouncer](https://www.pgbouncer.org/)
* [4-Масштабирование базы данных через шардирование и партиционирование](https://habr.com/ru/company/oleg-bunin/blog/309330/)
* [5-Принципы DRBD - Distributed Relicated Block Device)](https://russianblogs.com/article/9618107343/)


Полезные ссылки:
* [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats)
* [ALTER TABLE](https://postgrespro.ru/docs/enterprise/12/sql-altertable)
* [Partitioning in Postgres How Far We’ve Come](https://www.postgresql.eu/events/pgconfeu2019/sessions/session/2685/slides/225/pgconf-eu-2019.pdf)
* [CREATE TABLE](https://postgrespro.ru/docs/postgresql/10/sql-createtable#SQL-CREATETABLE-PARTITION)
* [Секционирование таблиц](https://postgrespro.ru/docs/postgresql/12/ddl-partitioning?lang=ru)
* [DBeaver Community Free Universal Database Tool](https://dbeaver.io/download/)
* [Запускаем PostgreSQL в Docker: от простого к сложному](https://habr.com/ru/post/578744/)
* [PARTITION OF таблица_родитель FOR VALUES указание_границ_секции](https://postgrespro.ru/docs/postgresql/10/sql-createtable#SQL-CREATETABLE-PARTITION)
* 


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
root@49db9913bea2:~# psql -U postgres -c "\?"
General
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display results in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send results to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store results in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [SEC]           execute query every SEC seconds

Help
  \? [commands]          show help on backslash commands
  \? options             show help on psql command-line options
  \? variables           show help on special variables
  \h [NAME]              help on syntax of SQL commands, * for all commands

Query Buffer
  \e [FILE] [LINE]       edit the query buffer (or file) with external editor
  \ef [FUNCNAME [LINE]]  edit function definition with external editor
  \ev [VIEWNAME [LINE]]  edit view definition with external editor
  \p                     show the contents of the query buffer
  \r                     reset (clear) the query buffer
  \s [FILE]              display history or save it to file
  \w FILE                write query buffer to file

Input/Output
  \copy ...              perform SQL COPY with data stream to the client host
  \echo [-n] [STRING]    write string to standard output (-n for no newline)
  \i FILE                execute commands from file
  \ir FILE               as \i, but relative to location of current script
  \o [FILE]              send all query results to file or |pipe
  \qecho [-n] [STRING]   write string to \o output stream (-n for no newline)
  \warn [-n] [STRING]    write string to standard error (-n for no newline)

Conditional
  \if EXPR               begin conditional block
  \elif EXPR             alternative within current conditional block
  \else                  final alternative within current conditional block
  \endif                 end conditional block

Informational
  (options: S = show system objects, + = additional detail)
  \d[S+]                 list tables, views, and sequences
  \d[S+]  NAME           describe table, view, sequence, or index
  \da[S]  [PATTERN]      list aggregates
  \dA[+]  [PATTERN]      list access methods
  \dAc[+] [AMPTRN [TYPEPTRN]]  list operator classes
  \dAf[+] [AMPTRN [TYPEPTRN]]  list operator families
  \dAo[+] [AMPTRN [OPFPTRN]]   list operators of operator families
  \dAp[+] [AMPTRN [OPFPTRN]]   list support functions of operator families
  \db[+]  [PATTERN]      list tablespaces
  \dc[S+] [PATTERN]      list conversions
  \dC[+]  [PATTERN]      list casts
  \dd[S]  [PATTERN]      show object descriptions not displayed elsewhere
  \dD[S+] [PATTERN]      list domains
  \ddp    [PATTERN]      list default privileges
  \dE[S+] [PATTERN]      list foreign tables
  \det[+] [PATTERN]      list foreign tables
  \des[+] [PATTERN]      list foreign servers
  \deu[+] [PATTERN]      list user mappings
  \dew[+] [PATTERN]      list foreign-data wrappers
  \df[anptw][S+] [PATRN] list [only agg/normal/procedures/trigger/window] functions
  \dF[+]  [PATTERN]      list text search configurations
  \dFd[+] [PATTERN]      list text search dictionaries
  \dFp[+] [PATTERN]      list text search parsers
  \dFt[+] [PATTERN]      list text search templates
  \dg[S+] [PATTERN]      list roles
  \di[S+] [PATTERN]      list indexes
  \dl                    list large objects, same as \lo_list
  \dL[S+] [PATTERN]      list procedural languages
  \dm[S+] [PATTERN]      list materialized views
  \dn[S+] [PATTERN]      list schemas
  \do[S+] [PATTERN]      list operators
  \dO[S+] [PATTERN]      list collations
  \dp     [PATTERN]      list table, view, and sequence access privileges
  \dP[itn+] [PATTERN]    list [only index/table] partitioned relations [n=nested]
  \drds [PATRN1 [PATRN2]] list per-database role settings
  \dRp[+] [PATTERN]      list replication publications
  \dRs[+] [PATTERN]      list replication subscriptions
  \ds[S+] [PATTERN]      list sequences
  \dt[S+] [PATTERN]      list tables
  \dT[S+] [PATTERN]      list data types
  \du[S+] [PATTERN]      list roles
  \dv[S+] [PATTERN]      list views
  \dx[+]  [PATTERN]      list extensions
  \dy[+]  [PATTERN]      list event triggers
  \l[+]   [PATTERN]      list databases
  \sf[+]  FUNCNAME       show a function's definition
  \sv[+]  VIEWNAME       show a view's definition
  \z      [PATTERN]      same as \dp

Formatting
  \a                     toggle between unaligned and aligned output mode
  \C [STRING]            set table title, or unset if none
  \f [STRING]            show or set field separator for unaligned query output
  \H                     toggle HTML output mode (currently off)
  \pset [NAME [VALUE]]   set table output option
                         (border|columns|csv_fieldsep|expanded|fieldsep|
                         fieldsep_zero|footer|format|linestyle|null|
                         numericlocale|pager|pager_min_lines|recordsep|
                         recordsep_zero|tableattr|title|tuples_only|
                         unicode_border_linestyle|unicode_column_linestyle|
                         unicode_header_linestyle)
  \t [on|off]            show only rows (currently off)
  \T [STRING]            set HTML <table> tag attributes, or unset if none
  \x [on|off|auto]       toggle expanded output (currently off)

Connection
  \c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}
                         connect to new database (currently "postgres")
  \conninfo              display information about current connection
  \encoding [ENCODING]   show or set client encoding
  \password [USERNAME]   securely change the password for a user

Operating System
  \cd [DIR]              change the current working directory
  \setenv NAME [VALUE]   set or unset environment variable
  \timing [on|off]       toggle timing of commands (currently off)
  \! [COMMAND]           execute command in shell or start interactive shell

Variables
  \prompt [TEXT] NAME    prompt user to set internal variable
  \set [NAME [VALUE]]    set internal variable, or list all if no parameters
  \unset NAME            unset (delete) internal variable

Large Objects
  \lo_export LOBOID FILE
  \lo_import FILE [COMMENT]
  \lo_list
  \lo_unlink LOBOID      large object operations

```



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
Создаем backup для БД `test_database`
```ps
root@49db9913bea2#pg_dump -U postgres -d test_database > test_database_dump.sql
```
Дорабатываем файл backup. Необходимо открыть файл в текстовом редактрое и добавить строчки:
```ps
--
-- Name: orders_1 unique_title_1; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.orders_1
    ADD CONSTRAINT unique_title_1 UNIQUE (title);

--
-- Name: orders_2 unique_title_2; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.orders_2
    ADD CONSTRAINT unique_title_2 UNIQUE (title);

```

Предварительная проработка вопроса
```ps
--
-- Name: orders_copy orders_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.orders_copy
    ADD CONSTRAINT orders_pkey PRIMARY KEY (id);

--
-- Name: orders_copy orders_pkey; Type: CONSTRAINT; Schema: public; Owner: postgres
--

CREATE INDEX ON orders ((lower(title)));



 делать через ALTER TABLE таблица ADD CONSTRAINT имя_органичения UNIQUE (колонка 1, колонка 2);

--
-- Name: orders_copy unique_title; Type: CONSTRAINT; Schema: public; Owner: postgres
--

ALTER TABLE ONLY public.orders_copy ADD CONSTRAINT unique_title UNIQUE (title);
```
#### Восстанавливаем данные в БД

Для проверки восстанавливаемости БД удаляем экземпляр БД
```ps
postgres=# drop database test_database;
DROP DATABASE
```
И создаем новый пустой экземпляр ЬД
```ps
postgres=# create database test_database;
CREATE DATABASE
```
Затем восстанавливаем данные из сохраненного и скорректированного дампа
```ps
postgres=# \q
root@49db9913bea2:~# 
root@49db9913bea2:~# psql -U postgres -d test_database -f /var/lib/postgresql/data/test_database_dump.sql
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
CREATE TABLE
ALTER TABLE
SET
CREATE TABLE
ALTER TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
ALTER TABLE
CREATE TABLE
ALTER TABLE
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 3
COPY 5
COPY 8
 setval 
--------
      8
(1 row)

ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE


```
БД восстановилась:
```ps
postgres=# \c test_database
You are now connected to database "test_database" as user "postgres".
test_database=# 
test_database=# 
test_database=# \dt
                  List of relations
 Schema |    Name     |       Type        |  Owner   
--------+-------------+-------------------+----------
 public | orders      | partitioned table | postgres
 public | orders_1    | table             | postgres
 public | orders_2    | table             | postgres
 public | orders_copy | table             | postgres
(4 rows)

```
Содержимое таблиц БД

```ps
test_database=# select * from orders;
 id |        title         | price 
----+----------------------+-------
  1 | War and peace        |   100
  3 | Adventure psql time  |   300
  4 | Server gravity falls |   300
  5 | Log gossips          |   123
  7 | Me and my bash-pet   |   499
  2 | My little database   |   500
  6 | WAL never lies       |   900
  8 | Dbiezdmin            |   501
(8 rows)

test_database=# 
test_database=# select * from orders_1;
 id |       title        | price 
----+--------------------+-------
  2 | My little database |   500
  6 | WAL never lies     |   900
  8 | Dbiezdmin          |   501
(3 rows)

test_database=# 
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
Проверяем свойства столбца ` title ` принимать новые значения.
Пробуем добавить в таблицу новую строку с новым  значением для поля ` title `
```ps
test_database=# insert into orders VALUES (9, 'My grand database', 600);
INSERT 0 1
```
Проверяем свойства столбца ` title ` принимать только уникальные значения.
Пробуем добавить в таблицу новую строку с повторяющимся значением из поля ` title `
```ps
test_database=# insert into orders VALUES (10, 'My little database', 750);
ERROR:  duplicate key value violates unique constraint "unique_title_1"
DETAIL:  Key (title)=(My little database) already exists.
test_database=# 

```
Вывод: повторяющее значение таблица не принимает, значит мы наблюдаем свойство уникальности значения столбца `title` 

---

