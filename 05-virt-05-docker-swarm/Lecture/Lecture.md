# Лекция по теме "5.5 Оркестрация кластером Docker контейнеров на примере Docker Swarm"

Олег
БукатчукОлег
Имя Фамилия
Букатчук
Software
Должность,
Architect компания
DevOps, crif.com
Skype
olegbukatchuk
Slack
Telegram

### План занятия
1. Введение. Возможности Docker Swarm
2. Архитектура Docker Swarm
3. Базовые команды Docker Swarm
4. Теорема CAP
5. Развёртывание стека микросервисов в Docker Swarm кластере
6. Итоги
7. Домашнее задание

### Введение.
Возможности Docker Swarm

#### Docker Swarm. 02:00
**Docker Swarm** — это система кластеризации для Docker, которая превращает набор Docker хостов в полноценный кластер, называемый Docker Swarm.
- Каждый хост, в составе такого кластера выступает в качестве, либо управляющей ноды (manager), либо рабочей (worker).
- В кластере должен быть, как минимум, один управляющий хост (manager).

#### Docker Swarm. 04:13
Теоретически, физическое расположение машин не имеет значения, однако, **желательно иметь все Docker-ноды внутри одной локальной сети.**
В противном случае, управление операциями или поиск консенсуса между несколькими управляющими нодами может занять значительное количество времени.
Начиная **с версии Docker 1.12, Docker Swarm уже интегрирован в Docker Engine** как Swarm-режим.
В более старых версиях необходимо было запускать **swarm-контейнер** на каждом из хостов для обеспечения функционала кластеризации.

#### Возможности Docker Swarm. 07:46
- Балансировка нагрузки Docker Swarm отвечает за балансировку нагрузки и назначение **уникальных DNS-имен**, чтобы приложение, развернутое в кластере, можно было использовать так же, как, если бы приложение было развернуто на одном Docker Engine хосте.
Другими словами, Docker Swarm может публиковать порты так же, как контейнер в Docker Engine, а затем **управляющая нода распределяет запросы между serviceами в кластере.**

#### Возможности Docker Swarm. 09:56
- Динамическое управление ролями: **manager/worker**
Docker-хосты могут быть добавлены Swarm кластеру без необходимости перезапуска кластера. Более того, роль узла (управляющий или рабочий) также может динамически меняться на лету.
**Для того чтобы динамически добавить/убрать роль manager нужно выполнить команду:**
```bash
# Добавление роли manager
$docker node promote <node name>

#Удаление роли manager
$docker node demote <node name>
```

#### Возможности Docker Swarm. 11:29
- Динамическое масштабирование сервисов
Каждый **service**, запущенный в Swarm кластере, может динамически масштабироваться, как в сторону увеличения, так и в сторону уменьшения **количества реплик*.
Управляющая нода (manager) заботится о добавлении или удалении контейнеров на рабочих узлах кластера.
```bash
#Добавление реплик сервиса
$docker service update --replicas=3 my-service

#Откат изменений (отмена последнего изменения конфигурации)
$docker service rollback my-service
```

#### Возможности Docker Swarm. 14:58
- Восстановление при отказе узлов 
Рабочие ноды постоянно контролируются управляющей нодой и, если какая-либо нода сбоит, то **новые задачи запускаются на других рабочих нодах** с целью обеспечения заявленного (желаемого) количество реплик.
Docker Swarm также позволяет **создавать несколько управляющих нод для предотвращения поломки кластера** в случае выхода из строя единственной управляющей ноды.
- Пояснение на 17:11:
  - Действительно отказоустойчивый кластер - это когда каждая роль соблюдена в количественном выражении по формуле "N+1", где N не меньше 2. Соответственно, только при наличии трех одновременно доступных серверов с каждой ролью - это та минимальная конфигурация для обеспечения такого требования как высокая доступность.

#### Возможности Docker Swarm. 18:45
- Обновления с задержкой (rolling updates)
Обновление сервисов может **применяться постепенно**. Например, если у нас есть 10 реплик, и мы хотим внести изменения (обновить версию нашего сервиса), мы можем **определить задержку между развертыванием** для каждой реплики.
В таком случае, когда что-то пойдет не так, **процесс обновления автоматически прерывается**, тем самым защищая нас от ситуации, когда в кластере не останется рабочих реплик.
- Пояснение на 21:40
  - В любой момент можно вручную сделать откат и прерывание обновления командой ` rollback `

### Архитектура Docker Swarm. 23:05
#### Архитектура Docker Swarm. 23:05
![12Архитектура-Docker-Swarm](/05-virt-05-docker-swarm/Lecture/img/12Архитектура-Docker-Swarm.png)
#### Архитектура Docker Swarm. 25:33
![13Архитектура-Docker-Swarm](/05-virt-05-docker-swarm/Lecture/img/13Архитектура-Docker-Swarm.png)
Пояснение на 27:30: балансировка нагрузок - это основная функция Оркестратора контейнеров
### Архитектура Docker Swarm. 30:27
![14Архитектура-Docker-Swarm](/05-virt-05-docker-swarm/Lecture/img/14Архитектура-Docker-Swarm.png)
### Архитектура Docker Swarm. 32:26
-Есть два типа выполнения сервисов:
  - Replicated. Он находится в стольких экземплярах, сколько мы задаем
  - Global. В этом режиме сервисы запускаются на всех нодах одновременно. Обычно режим Global используется для различных экспортеров, чтобы обеспечить мониторинг всего кластера. Также для всех сущностей, которые нужно чтобы они в моменте находились на каждой ноде, неважно Worker это или Manager. Самый типичный прмиер режима выполнения сервиса Global - это экспортеры для передачи метрик на сервер мониторинга.
![15Архитектура-Docker-Swarm](/05-virt-05-docker-swarm/Lecture/img/15Архитектура-Docker-Swarm.png)

### Сети в кластере Docker Swarm. 34:32
При разворачивании Swarm кластера на VM с публичными IP-адресами хорошей практикой является настройка правил брандмауэра для разрешения трафика Docker Swarm на каждом сервере перед созданием кластера.
Для успешного создания кластера необходимо, чтобы каждая VM могла связаться друг с другом по следующим протоколам и портам:
- TCP порт 2377 для обеспечения связи с целью управления кластером;
- TCP и UDP порт 7946 для связи между нодами;
- UDP порт 4789 для трафика overlay-сети.
Пояснение: необходимо физически разделять трафик гипервизоров и трафик пользователей

### Базовые команды Docker Swarm 40:10
#### Базовые команды Docker Swarm 40:23
- docker swarm init — инициализация кластера. 
Кластер будет инициализирован, как **single-mode instance**. Так же этой ноде будет автоматически присвоена роль **manager**. 
- [Подробнее](https://docs.docker.com/engine/reference/commandline/swarm_init/)
```bash
# Инициализация кластера Docker Swarm
$ docker swarm init --advertise-addr <ip address>
Swarm initialized: current node (bvz81updecsj6wjz393c09vti) is now amanager.
To add a worker to this swarm, run the following command: docker swarm join \ --token

SWMTKN-1-3pu6hszjas19xyp7ghgosyx9k8atbfcr8p2is99znpy26u2lkl-1awxwuwd3z9j1z3puu7rcgdbx \ <ip address>:2377
To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

#### Базовые команды Docker Swarm. 41:38
- docker swarm join — добавление в кластер новых серверов.
**ВАЖНО!!!** В зависимости от того, какой **ключ** указать вводимый в кластер сервер получит либо роль **worker**, либо роль **manager**.

- docker swarm join-token — вывод актуальных ключей для добавления нод в кластер. 
- [Подробнее](https://docs.docker.com/engine/reference/commandline/swarm_join/)

```bash
# Добавление ноды в кластер Docker Swarm
#По умолчанию добавляет роль worker показывает токен для роли worker
$ docker swarm join --token
SWMTKN-1-3pu6hszjas19xyp7ghgosyx9k8atbfcr8p2is99znpy26u2lkl-1awxwuwd3z9j1z3puu7
rcgdbx \
<ip address>:2377

#Показывает токен для роли worker
$ docker swarm join-token -q worker
SWMTKN-1-3pu6hszjas19xyp7ghgosyx9k8atbfcr8p2is99znpy26u2lkl-1awxwuwd3z9j1z3puu7
rcgdbx

#Показывает токен для роли manager
$ docker swarm join-token -q manager
SWMTKN-1-3pu6hszjas19xyp7ghgosyx9k8atbfcr8p2is99znpy26u2lkl-7p73s1dx5in4tatdymy
hg9hu2
```

#### Базовые команды Docker Swarm. 43:00
- docker swarm ca — просмотр и обновление сертификатов кластера. 
Кластер по-умолчанию **при инициализации создает цепочку сертификатов** для безопасной коммуникации и передачи данных между нодами. 
- [Подробнее](https://docs.docker.com/engine/reference/commandline/swarm_ca/)
```bash
# Просмотр и обновление сертификатов кластера Docker Swarm
$ docker swarm ca
-----BEGIN CERTIFICATE----- .... -----END CERTIFICATE-----
$ docker swarm ca --rotate
desired root digest: sha256:05da740cf2577a25224…
rotated TLS certificates: [=========================> ] 1/3 nodes
rotated CA certificates:
[>                                                    ] 0/3
nodes
```

#### Базовые команды Docker Swarm. 45:40
- docker swarm leave — удаление ноды из кластера.
**ВАЖНО!!!** Перед удалением ноды из кластера, во избежание простоев работающих сервисов, **нужно очистить ноду** от запущенных на ней сервисов. 
- [Подробнее](https://docs.docker.com/engine/reference/commandline/swarm_leave/)

```bash
# Очистка Docker Swarm ноды перед удалением из кластера
$ docker node update --availability drain node01
node01

# Удаление Docker Swarm ноды из кластера
$ docker swarm leave
Node left the default swarm.
```

#### Базовые команды Docker Swarm. 47:15
- docker node — набор команд для управления свойствами, ролями, атрибутами нод Docker Swarm кластера. 
- Доступны команды: 
   - docker node ls, 
   - docker node promote, 
   - docker node demote, 
   - docker node inspect, 
   - docker node ps, 
   - docker node rm,
   - docker node update 
 -  [Подробнее](https://docs.docker.com/engine/reference/commandline/node/)
 
```bash
# Добавление роли manager для 2-х Docker Swarm нод в работающем
кластере
$ docker node promote node02 node03
Node node02 promoted to a manager in the swarm.
Node node03 promoted to a manager in the swarm.
# Удаление роли manager для 2-х Docker Swarm нод в работающем
кластере
$ docker node demote node02 node03
Node node02 demoted to a manager in the swarm.
Node node03 demoted to a manager in the swarm.
```

#### Базовые команды Docker Swarm. 48:48
- docker service — набор команд для управления сервисами и их свойствами, работающими в Docker Swarm кластере.
- Доступны команды: 
  - docker service create, 
  - docker service inspect, 
  - docker service logs, 
  - docker service ps, 
  - docker service ls,
  - docker service rollback, 
  - docker service rm, 
  - docker service scale, 
  - docker service update . 
- [Подробнее](https://docs.docker.com/engine/reference/commandline/service/)
Создаются некие абстракции, которые называются сервисами
```bash
# Добавление сервиса nginx в количестве 3-х реплик и определение
критериев для целевых нод
$ docker service create \
--name web \
--replicas 3 \
--replicas-max-per-node 1 \
--constraint node.platform.linux==linux \
nginx:alpine
ID
b6lww17hrr4e
NAME
web
MODE
replicated
REPLICAS
3/3
IMAGE
nginx:alpine
PORTS
```

#### Базовые команды Docker Swarm. 51:26
- docker stack — набор команд для управления сервисами и их свойствами, в формате идентичном Docker Compose, но для Docker Swarm кластера. 
- Доступны команды: 
  - docker stack deploy, 
  - docker stack ls, 
  - docker stack ps, 
  - docker stack rm, 
  - docker stack services .

- [Подробнее](https://docs.docker.com/engine/reference/commandline/stack/)

```bash
# Деплой сервиса nginx с использованием конфигурационного Compose файла
$ docker stack deploy --compose-file docker-compose.yml nginx
Creating network nginx_nginx
Creating network nginx_default
Creating service nginx_nginx

$ docker stack rm netology
Removing service nginx_nginx
Removing network nginx_default
Removing network nginx_nginx
```

### Теорема CAP. 54:35
#### Теорема CAP
Теорема CAP (известная также как теорема Брюера) — эвристическое утверждение о том, что в любой реализации распределенных вычислений возможно обеспечить не более двух из трёх следующих свойств:
- Consistency (согласованность данных);
- Availability (доступность);
- Partition tolerance (устойчивость к разделению).

#### Теорема CAP
- **Согласованность данных** (англ. consistency) — во всех вычислительных узлах в один момент времени данные не противоречат друг другу;
- **Доступность** (англ. availability) — любой запрос к распределенной системе завершается корректным откликом, однако без гарантии, что ответы всех узлов системы совпадают;
- **Устойчивость к разделению** (англ. partition tolerance) — расщепление распределенной системы на несколько изолированных секций не приводит к некорректности отклика от каждой из секций.

#### 28Теорема CAP
![28Теорема-CAP](/05-virt-05-docker-swarm/Lecture/img/28Теорема-CAP.png)
#### 29Теорема CAP. 1:00:46
**CA** (Availability + Consistency – Parition tolerance), когда **данные во всех узлах кластера согласованы и доступны, но не устойчивы к разделению.**

Это означает, что реплики одной и той же информации, распределенные по разным серверам по отношению друг к другу, не противоречат друг другу и любой запрос к распределенной системе завершается корректным откликом.

#### Теорема CAP. 1:01:22
**CA** (Availability + Consistency – Parition tolerance). Такие системы возможны при поддержке **ACID**-требований к транзакциям (Атомарность, Согласованность, Изоляция, Долговечность) и абсолютной надежности сети.
За счет **ACID** реализуется такой функционал, как шардирование
На практике таких решений на основе кластерных систем управления базами данных почти не существует.
Для того, чтобы подобное решение обрело высокую доступность, нужна связка со сторонним демоном. Напрмер, для кластера БД Postgrees такой сторонней разработкой является утилита Patroni. Она сама следит за доступностью узлов и обеспечивает согласованность.


#### Теорема CAP. 1:03:20
CP (Consistency + Partition tolerance – Availability) в каждый
момент обеспечивает целостность данных и способна работать в
условиях распада в ущерб доступности, не выдавая отклик на
запрос.
Устойчивость к разделению требует дублирования изменений во
всех узлах системы, что реализуется с помощью распределенных
пессимистических блокировок для сохранения целостности.

#### Теорема CAP. 1:04:35
CP (Consistency + Partition tolerance – Availability).
По сути, CP – это система с несколькими синхронно
обновляемыми мастер-базами. Она всегда корректна,
отрабатывая транзакцию, только в том случае, если изменения
удалось распространить по всем серверам.

#### Теорема CAP. 1:05:09
AP (Availability + Partition tolerance – Consistency) **не гарантирует целостность данных, обеспечивая их доступность и устойчивость к разделению**, например, как в распределенных веб-кэшах и DNS.
Считается, что большинство NoSQL-СУБД относятся к этому классу систем, обеспечивая лишь некоторой уровень согласованности данных в конечном счете (eventually consistent).

#### Теорема CAP. 1:07:02
AP (Availability + Partition tolerance – Consistency).
Таким образом, AP-система может быть представлена кластером из нескольких узлов, каждый из которых **может принимать данные, но не обязуется в тот же момент распространять их** на другие сервера.

### Развертывание стека микросервисов в Docker Swarm кластере. 1:08:35

С 1:09:43 по 1:23:40 - технические сбои. Плохая картинка, разговор ни о чем.

### Практическая часть
#### 1. Авторизуемся в Yandex.Cloud.
#### 2. Создаём сеть и подсеть, чтобы собрать образ ОС с помощью Packer и запускаем сборку образа.
- Создался образ диска - 1:24:05
#### 3. Удаляем подсеть и сеть, которую использовали для сборки образа ОС.
- 1:24:35. Из директории ` ../packer ` переходим в директорию ` ../terraform `
- У нас появилось 6 шаблонов для 6 ВМ
- Появился новый файл ` inventory ` с динамическим шаблоном
#### 4. Создаём 6 виртуальных машин с помощью Terraform.
- 1:27:40. Запуск ` terraform init ` , ` terraform validate ` , ` terraform plan `
- 1:28:34. ` terraform apply -auto-approve `
- 1:29:06 - удаление сетей.  ` yc vpc subnet delete --name my-subnet-a && yc vpc network delete --name mnet `
- 1:29:16. ` terraform apply -auto-approve `. Ошибки при создании сетей. Причина - не изменил ID на актуальные в файле ` variables `
- 1:29:50  ` terraform destroy -auto-approve ` Удаление ранее созданных ВМ
- 1:29:55. Корректирование файла ` variables `
- 1:30:00. Повторный запуск команд ` terraform init ` , ` terraform validate ` , ` terraform plan ` , ` terraform apply -auto-approve `
#### 5. Создаём Docker Swarm кластер из виртуальных машин, созданных на предыдущем шаге.

#### 6. Запускаем деплой стека приложений.
- 1:35:23 Запустился Ansible
- 1:38:00 О шаге синхронизации директорий
- 1:38:55 Что происходит при деплое на примере файла ` swarm-deploy-stack.yml `
- 1:39:10. Разбор файла ` swarm-deploy-stack.yml `
- 1:39:46 Окончание выполнения команды ` terraform apply -auto-approve `
- 1:39:50 Контроль автоматического заполнения файла ` inventiry ` теми IP адресами, которые появились в выводе при окончании отработки команды ` terraform apply -auto-approve `
#### 7. Проводим стресс тест Docker Swarm кластера.
- 1:41:00 Заходим на страницу с сервисом Графана
- 1:44:22
- 1:45:00 Заходим на одну из нод. Смотрим вывод ` docker node ls `
-  1:46:36 Проведение стресс-теста. Перезагрузка ноды 01. Наблюдаем смену лидера у менеджеров
#### 8. Удаляем всё, чтобы не тратить деньги!
- 1:51:55 Демонстрация того как узнать имя задеплоиного стека сервисов ` docker stack ls ` , их состояние ` docker stack ps swarm_monitoring `

### Итоги

Сегодня мы:
- узнали о преимуществах технологии Docker Swarm;
- рассмотрели архитектуру Swarm кластера;
- научились создавать Docker Swarm;
- научились создавать простейший pipeline деплоя используя Terraform и Ansible;
- создали кластер высокой доступности на основе Docker Swarm и развернули в нём стек микросервисов, устойчивый к отказам виртуальных машин.

### Полезные материалы. 1:55:55
- [In Search of an Understandable Consensus Algorithm(Extended Version)](https://raft.github.io/raft.pdf)
- [Raft (визуализация)](http://thesecretlivesofdata.com/raft/)
- [Gossip](https://en.wikipedia.org/wiki/Gossip_protocol)

### Домашнее задание
Давайте посмотрим ваше домашнее задание.
● Вопросы по домашней работе задавайте в чате мессенджера
Slack.
● Задачи можно сдавать по частям.
● Зачёт по домашней работе проставляется после того, как
приняты все задачи.
### Задавайте вопросы и
пишите отзыв о лекции!
Олег Букатчук
olegbukatchuk
