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
- подключения к БД
- вывода списка таблиц
- вывода описания содержимого таблиц
- выхода из psql
