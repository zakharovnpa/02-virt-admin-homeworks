## Ход выполнения Задания №1

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

