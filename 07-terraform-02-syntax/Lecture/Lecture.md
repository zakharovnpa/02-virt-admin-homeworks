## Облачные провайдеры и синтаксис Терраформ

Сергей
АндрюнинСергей Андрюнин
DevOps-инженер
RTLabs
Сергей Андрюнин

### 2План занятия
1. Облачные провайдеры
2. Amazon EC2
3. Синтаксис Terraform
4. Структура проекта
5. Итоги
6. Домашнее задание
3Облачные провайдеры

### 4AWS
- Популярное решение на зарубежном рынке
- Очень большое количество сервисов
- В первый год использования есть бесплатный тариф:
https://aws.amazon.com/free/.

### 5Yandex.Сloud
- Популярное решение в русскоязычном сегменте
- Документация на русском языке
- Достаточное количество сервисов

### - 00:05:10 - о том, что лучше поднять свое облако на
  - OpenStack
  - Open Nebule
  - ESXi
  - KVM
  - Baremetal Kubernetes
  чем заезжать в облако Яндекс

### 6План действий
- Рассмотрим работу с ресурсами облачных провайдеров через командную строку и веб-консоль
- Поймем, в чем сложности такого подхода
- Разберемся, как Terraform упростит нам жизнь

### 7Регистрация в AWS
- Кредитная карта нужна только для регистрации
- Пользуемся бесплатным тарифом, который доступен год после регистрации
- Можно зарегистрировать отдельный «учебный» аккаунт на email типа «yourname**+netology**@gmail.com»

### 8Регистрация в Yandex.Cloud
- Есть бесплатный пробный период
- Далее каждому студенту будут выданы промокоды

### 9Элементы управления AWS

### 10Элементы управления Яндекс.Cloud

### 11Регионы и зоны доступности AWS
AWS охватывает 77 зон доступности в 24 географических регионах по всему миру.

### 12Установка cli клиентов
- При помощи менеджера пакетов apt, brew, ...
- AWS: Скачать исходники https://aws.amazon.com/cli/
- Yandex: https://cloud.yandex.ru/docs/cli/quickstart

### 13VPC (Virtual Private Cloud)
Это логически изолированный раздел облака, в котором можно запускать ресурсы в самостоятельно заданной виртуальной сети.
Таким образом можно полностью контролировать среду виртуальной сети, в том числе выбирать собственный диапазон
IP‑адресов, создавать подсети, а также настраивать таблицы маршрутизации и сетевые шлюзы.

### 14AWS Identity and Access Management (IAM)
IAM – это место где происходит управление учетными записями
пользователей и их правами.
- Создаем отдельного пользователя для дальнейшей работы
- Нужно получить:
  - идентификатор ключа доступа: Access Key ID,
  - секретный ключ доступа: Secret Access Key

### 15Yandex.Cloud IAM для Terraform. 21:21 от начала лекции
[Инструкция для получения токена:](https://cloud.yandex.ru/docs/iam/operations/iam-token/create)

Этот токен также подходит для работы Terraform


### 16Политика (policy) IAM. 22:05 от начала лекции
Политика IAM – это документ в формате JSON, который определяет, что пользователю позволено, а что — нет.
Назначим нашему пользователю:
- AmazonEC2FullAccess
- AmazonS3FullAccess
- AmazonDynamoDBFullAccess
- AmazonRDSFullAccess
- CloudWatchFullAccess
- IAMFullAccess

### 17Регистрируем этого пользователя локально. 23:30 от начала лекции
Чтобы консольный клиент AWS и Terraform получили доступ
к нашему аккаунту создаем переменные окружения:
```bash
$ export AWS_ACCESS_KEY_ID=(your access key id)
$ export AWS_SECRET_ACCESS_KEY=(your secret access key)
```
Яндексовая тулза использует те же самые вещи. Те же самые названия переменных будут работать.
```bash
$ export AWS_ACCESS_KEY_ID=(your access key id)
$ export AWS_SECRET_ACCESS_KEY=(your secret access key)
```

### 18Amazon EC2

### 19Amazon Elastic Compute Cloud (Amazon EC2)
Это веб‑сервис, предоставляющий безопасные масштабируемые вычислительные ресурсы в облаке.
Позволяет выбрать:
- тип и количество ядер процессора,
- объем оперативной памяти,
- хранилища,
- акселераторы,
- и другое.

### 20Создание EC2 через веб интерфейс. 24:50
[Ссылка для создания](https://us-west-2.console.aws.amazon.com/ec2/v2/home)

Это то место, где лежат наши ВМ


### 21Создание EC2 через консоль. 25:05

[Ссылка для создания](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/opsworks/create-instance.html)

```bash
aws ec2 create-instance

[--source-dest-check | --no-source-dest-check]
[--attribute <value>] 
[--block-device-mappings <value>]
[--disable-api-termination | --no-disable-api-termination]
[--dry-run | --no-dry-run] 
[--ebs-optimized | --no-ebs-optimized]
[--ena-support | --no-ena-support] 
[--groups <value>]
--instance-id <value> 
[--instance-initiated-shutdown-behavior <value>]
[--instance-type <value>] 
[--kernel <value>]
[--ramdisk <value>] 
[--sriov-net-support <value>] 
[--user-data <value>]
[--value <value>] 
[--cli-input-json | --cli-input-yaml]
[--generate-cli-skeleton <value>] 
[--cli-auto-prompt <value>]
```

### 22Основные параметры EC2. 27:40
Что нужно знать для создания инстанса:
- тип (процессор, память),
- идентификатор виртуального приватного облака,
- способ автоскейлинга,
- операционная система,
- идентификатор образа (ami),
- ключ доступа по ssh,
- зона доступности,
- идентификатор подсети,
- тип подключенных хранилищ,
- … и еще десяток параметров.

### 23А теперь нужно изменить инстанс
- Иногда необходимо предварительно остановить инстанс
- Иногда пересоздать
- Хорошо бы понять, что конкретно будет изменено
- Часто надо привести инстанс в исходное состояние после ручных правок

### 24Как это сделать?
- Зайти в веб интерфейс и проверять все параметры?
- Через консоль выполнить:
  - describe,
  -  сравнить с целевыми (исходными) значениями,
  -  modify.
- Хорошо бы понять, что конкретно будет изменено (типа git diff)
- Часто надо привести инстанс в исходное состояние после ручных правок

### 25Другими словами...
Надо воспользоваться командами:
```bash
aws ec2 create-key-pair
aws ec2 create-instance
aws ec2 create-tags
aws ec2 create-volume
aws ec2 describe-key-pair
aws ec2 describe-instances
aws ec2 describe-tags
aws ec2 describe-volume
....
```

### 26Синтаксис Terraform. 31:18

### 27Terraform
Terraform – это просто API-клиент. Это бинарник, написанный на языке GO от компании Hashicorp.
Это синтаксический анализатор кода на языке HCL. Скоро будет HCL2.
Террафрм осуществляет свои действия с помощью провайдеров.
Terraform-провайдеры «знают» все эти команды и умеют приводить состояние ресурсов к описанному в своих конфигурационных файлах.
Провайдеры могут работать как с любым клиентом: cli, http, их комбинациями и другими.

### 28Terraform-провайдеры
terraform.io/docs/providers/index.html
В официальном репозитории около 150 штук. Плюс много неофициальных, и можно достаточно просто создавать собственные.

### 29Блоки
Все конфигурации описываются в виде блоков.
```tf
resource "aws_vpc" "main" {
      cidr_block = var.base_cidr_block
}

тип "идентификатор" "имя" {
      название_параметра = выражение_значение_параметра
}
```
### 30Блок провайдеров - 00:42:25
registry.terraform.io/providers/hashicorp/aws/latest/docs
```tf
provider "aws" {
    region = "us-east-1"
}
```
### 31Блок требований к провайдерам
Блок «terraform» для указаний версий провайдеров и бэкэндов.
```tf
terraform {
    required_providers {	# используемый провайдер
        aws = {		# название провайдера
            source = "hashicorp/aws"		#откуда его взять
            version = "~> 3.0"
    }
  }
}
```
### 32Блок ресурсов
registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance
Ресурс **aws_instance** – это экземпляр ec2
```tf
resource "aws_instance" "web" {	# ресурс, имя ресура, которое мы прсвом
   ami = data.aws_ami.ubuntu.id		# образ, используемый для создания ВМ
      instance_type = "t3.micro"	# тп ресурса, определенный облачным провайдером. Пож типом прячутся параметры проц, памят, размера диска и др. 
}
```
### 33Блок внешних данных	- 00:43:10
Для того что бы прочитать данные из внешнего API и использовать для создания других рессурсов.
Use this data source to get the access to the effective Account ID, User ID, and ARN in which Terraform is authorized.
[Data Source: aws_caller_identity](registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)
```hcl
data "aws_caller_identity" "current" {}

// data.aws_caller_identity.current.account_id
// data.aws_caller_identity.current.arn
// data.aws_caller_identity.current.user_id
```
Здесь вернется инфа о том, под какой УЗ вы подключены к облаку



### 34Блок переменных	- 00:43:35
Каждый модуль может зависеть от переменных.
```tf
variable "image_id" {
    type = string
}

resource "aws_instance" "example" {
      instance_type = "t2.micro"
      ami           = var.image_id  # для обращеня к переменной указываем var, точку  имя переменной image_id
}
```
### 35Блок переменных	- 00:44:00
Структура переменной может быть достаточно сложной.
```tf
variable "availability_zone_names" {
  type = list(string)
  default = ["us-west-1a"]
}

variable "docker_ports" {
  type = list(object({
    internal = number
    external = number
    protocol = string
  }))
  
default = [
  {
    internal = 8300
    external = 8300
    protocol = "tcp"
  }
 ]
}
```
### 36Типы переменных	- 00:44:25
```
Примитивные типы:
● string
● number
● bool
Комбинированные типы:
● list(<TYPE>)
● set(<TYPE>)
● map(<TYPE>)
● object({<ATTR NAME> = <TYPE>, ... })
● tuple([<TYPE>, ...])
```

### 37Валидация переменных	- 00:44:45

Особенно важно для повторно используемых модулей.
```tf
variable "image_id" {
  type = string
  description = "The id of the machine image (AMI) to use
for the server."

  validation {
    condition = length(var.image_id) > 4 &&
substr(var.image_id, 0, 4) == "ami-"

    error_message = "The image_id value must be a valid AMI
id, starting with \"ami-\"."
  }
}
```
Необходмо для валдац данных, которые мы передаем. В этом примере показана проверка того, что в выводе имени дректории будет более 4 знаков и первые 4 знака будут ami-


### 38Блок output	- 00:45:30
Для того чтобы разные модули могли использовать результат
работы друг друга.
```tf
output "instance_ip_addr" {
 value       = aws_instance.server.private_ip
 description = "The private IP address of the main server instance."

 depends_on = [

# Security group rule должна быть создана перед тем как
можно будет использовать этот ip адрес, иначе сервис будет
недоступен
    aws_security_group_rule.local_access,
  ]
}
```
### 39Локальные переменные	- 00:46:50
Могут быть использованы внутри модуля сколько угодно раз.
```tf
locals {
    service_name = "forum"	# будем тегировать все образы
    owner         = "Community Team"	# владелец будет этот
}

locals {
    instance_ids = concat(
    aws_instance.blue.*.id, aws_instance.green.*.id
)

common_tags = {
    Service = local.service_name
    Owner   = local.owner
  }
}
```

### 40Комментарии	- 00:47:14
Terraform поддерживает несколько видов комментариев:
```bash
# начинает однострочные комментарии;
// также однострочные комментарии;
/* и */ для обозначения многострочных комментариев.
```

### 41Структура проекта		- 00:47:40

### 42Структура каталогов
- /main.tf	- заглавный файл
- /any_ﬁle.tf	- файлы с переменным, и др. парамтерами
- /modules/
- /modules/awesome_module/
- /modules/awesome_module/main.tf
- /modules/awesome_module/any_other_ﬁle.tf
- /modules/next_module/
- /modules/next_module/main.tf
- /modules/next_module/any_other_ﬁle.tf

### 43Структура файлов	- 00:48:37
- main.tf
- variables.tf
- outputs.tf
- any_other_ﬁles.tf

### 44Итоги	- 00:49:12

### 45Итоги
Сегодня мы:
- Познакомились с облачными провайдерами AWS и Yandex.Cloud$
- Познакомились с базовым синтаксисом Terraform;
- Узнали, как создавать виртуальный инстанс ec2:
  - через веб интерфейс,через cli консоль,
  - при помощи Terraform.

### Продолжение темы. Дополнительная информация.	- 00:49:20

#### Описание создания новостного агрегатора
- Здесь расположен репозиторий с новостным агрегатором: https://gitlab.com/k11s-os

### - 00:52:10 Создание ВМ в Я.О веб интерфейс
### - 00:56:30 Создание ВМ в консольной утилите
- `compute instance create`
- 00:58:25 - `yc compute instance list`
### - 00:59:50 Big Demo сервса агрегатора новостей 
[Директория с агрегатором новостей](https://gitlab.com/k11s-os/news-app-demo/-/tree/main/)
- 01:00:40 - описание файлов агрегатора
- 01:01:50 - файлы на Go
- 01:02:30 - описание структуры [файла для CI](https://gitlab.com/k11s-os/news-app-demo/-/blob/main/.gitlab-ci.yml) `.gitlab-ci.yml`
- 01:03:00 - про создане образа Packer-ом
- 01:05:50 - про работу Terraform. О структуре проекта
- 01:06:30 - main.tf
- 01:07:00 - vars.tf
- 01:07:50 - в файле `main.tf` ВМ называются `module`
- 01:09:15 - про [модули](https://gitlab.com/k11s-os/infrastructure-as-code/-/tree/main/terraform/modules)
- 01:09:20 - про [модуль iam для K8s](https://gitlab.com/k11s-os/infrastructure-as-code/-/blob/main/terraform/modules/iam/service-accounts.tf)
- 01:09:35 - [instance.tf ](https://gitlab.com/k11s-os/infrastructure-as-code/-/blob/main/terraform/modules/instance/instance.tf)
```tf
variable image { default =  "centos-8" }
variable name { default = ""}
variable description { default =  "instance from terraform" }
variable instance_role { default =  "all" }
variable users { default = "centos"}
variable cores { default = ""}
variable platform_id { default = "standard-v1"}
variable memory { default = ""}
variable core_fraction { default = "20"}
variable subnet_id { default = ""}
variable nat { default = "false"}
variable instance_count { default = 1 }
variable count_offset { default = 0 } #start numbering from X+1 (e.g. name-1 if '0', name-3 if '2', etc.)
variable count_format { default = "%01d" } #server number format (-1, -2, etc.)
variable boot_disk { default =  "network-hdd" }
variable disk_size { default =  "20" }
variable zone { default =  "" }
variable folder_id { default =  "" }

terraform {
  required_providers {
    yandex = {
      source  = "yandex-cloud/yandex"
      version = "0.61.0"
    }
  }
}

data "yandex_compute_image" "image" {
  family = var.image
}

resource "yandex_compute_instance" "instance" {
  count = var.instance_count
  name = "${var.name}-${format(var.count_format, var.count_offset+count.index+1)}"
  platform_id = var.platform_id
  hostname = "${var.name}-${format(var.count_format, var.count_offset+count.index+1)}"
  description = var.description
  zone = var.zone
  folder_id = var.folder_id

  resources {
    cores  = var.cores
    memory = var.memory
    core_fraction = var.core_fraction
  }
  boot_disk {
    initialize_params {
      image_id = data.yandex_compute_image.image.id
      type = var.boot_disk
      size = var.disk_size
    }
  }
  network_interface {
    subnet_id = var.subnet_id
    nat       = var.nat
  }

  metadata = {
    ssh-keys = "${var.users}:${file("~/.ssh/id_rsa.pub")}"
  }
}


```

### Про Ansible  - 01:11:35
- 01:11:35 - создание динамческого инвентори для Ansible
  - сейчас в файле inventory/host пусто (empty). Мы значально не знаем какие у наших создаваемых ВМ будут ip адреса.
  - для того, чтобы получить ip адреса создаваемых ВМ есть лайфхак: если воспользоваться командой (преподаватель сказал утилитой) `yc compute instance list --format=yaml --folder-name={{yc_project_name}}` и передать в формате YAML в дректорию `{{yc_project_name}}`
```
вывод команды
```
  - соответственно этот файл мы можем распарсить
- Пример таски из файла site.yaml для создания динамческого инвентори 
```yml
---
- hosts: localhost
  become: false
  tasks:
    - name: get instances in yandex cloud
      shell: yc compute instance list --format=yaml --folder-name={{yc_project_name}}
      register: yc_instances    # записать в переменную yc_instances

    - set_fact:
        _yc_instances: '{{yc_instances.stdout | from_yaml }}'   # список на основе вывода переменной yc_instances

# Строки кода в продолжении таски для того, чтобы увидеть что происходит при распарсивания файла с выводом команды
# на 01:23:33 будет показан вывод результатов

    - debug:
        msg: "{{item['network_interfaces'][0]['primary_v4_address']['one_to_one_nat']['address']}}"
      with_list: '{{_yc_instances}}'
      debugger: on_failed

```
- 01:12:30 - показано как создавать hosts 
```yaml
 - name: Add host to multiple groups
      add_host:
        hostname: "{{item['network_interfaces'][0]['primary_v4_address']['one_to_one_nat']['address']}}"  # взять публичный адрес, протегроваться
 # hostname: "{{item['network_interfaces'][`tag`][0]['primary_v4_address']['one_to_one_nat']['address']}}"  # где-то в этой строке надо добавить тег
        
        groups:
          - balancers   # добавить в группу balancers
          - news        # добавить в группу news
      with_list: '{{_yc_instances}}'  # со списком, который мы получли выше

```
- 01:13:00 - о том что для разных групп надо раскатить или ngnix или app. надо назначать через grep (через description назначать), а раньше можно было через тэги
- мы тегируемся и добавляем ВМ в группу balancers или news

```yml
- hosts: balancers
  become: yes
  roles:
    - { role: nginx }

- hosts: news
  roles:
    - { role: app }

```
- 01:13:40 - как у нас выглядит app
  - в папке config есть директория с названем среды и названием роли balancer, который нклудит conf.d

``` 
 infrastructure-as-code/ansible/config/demo/balancers/nginx.conf.j2
```

- передаем файл параметров nginx.conf . это обычная джинджа - файл шаблона
```
worker_processes  2;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    log_format json escape=json '{"created_at": "$time_iso8601", '
                            '"app": "rsa_balancer", '
                            '"remote_addr_ip": "$remote_addr", '
                            '"remote_user": "$remote_user", '
                            '"body_bytes_sent": "$body_bytes_sent", '
                            '"request_time": "$request_time", '
                            '"status": "$status", '
                            '"request": "$request_uri", '
                            '"request_method": "$request_method", '
                            '"request_body": "$request_body", '
                            '"http_referrer": "$http_referer", '
                            '"http_user_agent": "$http_user_agent", '
                            '"message": "$time_iso8601 $remote_addr $remote_user $body_bytes_sent $request_time $status $request $request_method $http_referer $request_body $http_user_agent" }';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    gzip  on;

    include /etc/nginx/conf.d/*.conf;
    }

```
- инклудим этот шаблон файла:
```
 infrastructure-as-code/ansible/config/demo/balancers/conf.d/news-app.conf.j2
```
- у нас все динамика, все по феншую и по красоте
```
#{{ ansible_managed }} last deploy by {{ ansible_user_id }} on {{ ansible_date_time.date }} {{ ansible_date_time.hour }}:{{ ansible_date_time.minute }}

{% for upstream in upstreams.values() %}
upstream {{upstream.name}} {
{% for option in upstream.options %}
    {{option}};
{% endfor %}
{% for server in upstream.servers %}
{% if exclude_node not in server %}
    server {{server}} ;
{% endif %}
{% endfor %}
}
{% endfor %}



server {
        listen 80 default;
        server_name {{server_name}};

        client_max_body_size 50M;
        charset utf-8;
        proxy_buffering off;
        proxy_http_version 1.1;

        proxy_connect_timeout   10s;
        proxy_send_timeout              300s;
        proxy_read_timeout              300s;
        send_timeout                    300s;

        gzip on;
        gzip_comp_level 5;
        gzip_proxied any;
        gzip_types text/plain text/xml text/css application/javascript application/x-javascript text/javascript application/xml+rss text/json application/json;

        proxy_set_header  Host               $host;
        proxy_set_header  Connection "";

        access_log      {{ access_log }};
        error_log       {{ error_log }};

{% for location in locations.values() %}
        location {{location.name}} {
        {% for option in location.options %}
            {{option}} ;
        {% endfor %}
        {% if location.proxy_pass|length > 1 %}
            proxy_pass {{ location.proxy_pass }} ;
        {% endif %}
}
{% endfor %}
}

```
```
infrastructure-as-code/ansible/config/demo/news/systemd/app.service.j2
```
```
# {{ansible_managed}}
[Unit]
Description={{service}}
After=syslog.target network.target

[Service]
Type=simple
# Set Environment for APP

Environment=NEWS_APP_BIND_ADDR={{news_app_bind_addr | default("127.0.0.1:8080")}}
Environment=NEWS_APP_NEWS_LANG={{news_app_news_lang | default("ru")}}
Environment=NEWS_APP_API_KEY={{news_app_api_key | default("lalalalalal")}}

WorkingDirectory=/opt/{{service}}/current

ExecStart=/opt/{{service}}/current/{{app_startup_command}}    # для хранения несколькх версий на тачке
User={{app_user}}
Group={{app_user}}

[Install]
WantedBy=multi-user.target

```
- 01:14:35 - в инвентори у нас лежит `infrastructure-as-code/ansible/inventory/demo/group_vars/all.yml`
```yml
env: demo
yc_project_name: "{{ lookup('env','ENV') }}"
ansible_user: centos
log_root: "/var/log/{{ service }}"
custom_nginx: true
env_asserts:    # это подготовлено на будущее, чтобы работало CI/CD
  - APP_VERSION   
  - SERVICE
  - CI_PROJECT_ID

users:
  # Sergey Andryunin
  - username: sergey.andryunin
    state: present
    key: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC6H4lEXMWhEaUXl0hq7h3oIlBSQMcmllMSyS7Hb4NKPk9vHL+yr/z3yaqHXi5RzI3PUTg4b7fBaveJx57CKN0NxI+ws+4do8SUf1T0TsxDNIwp1AqaepS0srvAIEbX8Ofgj6AGavfbSaJAJmfUswgRB3BieYyqMZkLzQUKDTw/xYjRzoGTPK94L+AkO+Bh0rY5goAtK9RpoJGergBHojDIr9KeIuwBmApMeWuoWf2v2CbP0O5+FF7QmzbF/haMm/KeXgvc1mUL2mX+AAUPfvPL9uc+5dujvsZwC+uJqEgnMmemxO9vAP2FgvmswsB8ybITC+fv79KeZ/ZsZ1o3+x16apKE3rY0+vgynf/IK4iraoZre3FB84cOUQM9xjVO3m7md/os/oexLbYq+HZRcnDm8CIe+N8GbXhn4KldCo6m2k8wYS+FPeOxudi0mg5PM3O1FuCFUIN6MsggRjZV3QeuQui2TpqMk94KpIsfXwDhzrH7ldKvjudfzcax9lwjl/8= s.andryunin@fedora-work

```
- 01:15:25 - для балансровщика в инвентори у нас лежит `infrastructure-as-code/ansible/inventory/demo/group_vars/balancers.yml`

```yml
server_name: news-app-demo
access_log: /var/log/nginx/access.log main
error_log: /var/log/nginx/error.log warn
exclude_node: nothing   # указание на отулючение ноды из балансировки при канареечном обновлении

nginx_official_repo_mainline: true    #спользование офциальной репы

nginx_config_files:
  - news-app.conf

upstreams:    # для того, чрбы спрятать наше приложене за ngnix, чтобы он не торчал голой попой в Интернет
  news-app:
    name: news-app
    options:
      - keepalive 50
    servers:
      - 127.0.0.1:8080 max_fails=10 fail_timeout=10s

locations:
  root:
    name: /
    options:
      - proxy_set_header    Host                $host
      - proxy_set_header    X-Real-IP           $remote_addr
      - proxy_set_header    X-Forwarded-Host    $host
      - proxy_set_header    X-Forwarded-Server  $host
      - proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for
      - proxy_redirect      off
      - proxy_next_upstream error timeout http_502 http_503 http_500 http_504 non_idempotent
      - proxy_next_upstream_tries 2
    proxy_pass: http://news-app

```
- 01:17:13 - для нашего приложения в инвентори у нас лежит `infrastructure-as-code/ansible/inventory/demo/group_vars/news.yml`

```yml
app_user: newsapp
app_group: newsapp
keep_releases: 3
service: "{{ lookup('env','SERVICE') }}"
app_version: "{{ lookup('env','APP_VERSION') }}"
app_startup_command: "news-demo"
app_root: "/opt/{{ service }}"
app_path: "{{app_root}}/releases/{{app_version}}"
app_url: "https://gitlab.com/api/v4/projects/{{ lookup('env','CI_PROJECT_ID') }}/packages/generic/news-app-demo/{{ app_version }}" # путь у пакетнице
artifacts_name:
  - "news-app-demo.tar.gz"
artifact_name: "news-app-demo.tar.gz"
private_gitlab_token: "{{ lookup('env','CI_JOB_TOKEN') }}"

systemd: true
app_services_to_copy:
  - app.service
app_services_to_start:
  - app.service

shared_paths:
  - { path: "{{ app_root }}/current", src: "{{ app_root }}/releases/{{app_version}}" }

news_app_bind_addr: 127.0.0.1:8080
news_app_news_lang: ru
news_app_api_key: a0bd1250692648c79515de6be5f41dcc


```
- 01:19:20 - о ролях
- 01:20:30 - Makefile

```sh
ENV?=default

all: init workspace plan apply pause deploy

init:
	cd ./terraform/demo && terraform init

workspace:
	cd ./terraform/demo && terraform workspace new ${ENV}

set_workspace:
	cd ./terraform/demo && terraform workspace select ${ENV}

plan: set_workspace
	cd ./terraform/demo && terraform plan

apply: set_workspace
	cd ./terraform/demo && terraform apply -auto-approve

destroy: set_workspace
	cd ./terraform/demo && terraform destroy -auto-approve

clean:
	cd ./terraform/demo &&  rm -f terraform.tfplan
	cd ./terraform/demo &&  rm -f .terraform.lock.hcl
	cd ./terraform/demo &&  rm -fr terraform.tfstate*
	cd ./terraform/demo &&  rm -fr .terraform/

pause:
	echo "Wait for 60 seconds stupid Yandex Cloud creating a VM's..."
	sleep 60
	echo "May be created? Ok, run an ansible playbook..."
deploy:
	cd ./ansible && source .env.news-app && ansible-playbook -i inventory/demo site.yml

reconfig:
	cd ./ansible && source .env.news-app && ansible-playbook -i inventory/demo site.yml -t config

```
- 01:22:30 - запуск команды `make all` создаем ВМ в облаке
- 01:23:33 - ! показан вывод результатов таски для создания днамческого инвентори. Яндекс отдает какие у него есть инстансы.
- 01:24:20 - чтобы плейбук делал ретраи если в облаке не успевается запустться демон ssh. Или добавить wait
- 01:27:50 - make destroy  - удаляем ВМ из облака
- 01:28:50 - добавление ресурсов для ВМ
- 01:30:00 - про добавление wait для ожидания запуска демона ssh
- 01:31:00 - о том ка надо раскидывать ресурсы по конфгурации
- 01:45:35 - о том как происходит роллбэек. Что такое L-config - это тегированные таски только для того чтобы переконфгурть приложение
- 01:45:55 - том что такое роль Ansistrana. ansistrana deploy, ansistrana rollback
- 01:46:15 - о ролях для развертываня приложения. Но файлы .py преподаватель нам не дал!
Таска для создания DNS в Яндекс облаке
* infrastructure-as-code/ansible/roles/nginx/tasks/config_dns_discovery.yml
```yml
- block:
    - name: Add vts-exporter dns srv records Yandex Cloud
      script: scripts/ipa_dns_record_add.py	#
      environment:
        IPA_ENDPOINT: "{{ _ipa_host }}"
        IPA_USER: "{{ _ipa_user.user_input | default(lookup('env','IPA_USER')) }}"
        IPA_PASS: "{{ _ipa_pass.user_input | default(lookup('env','IPA_PASS')) }}"
        DNS_ZONE_NAME: "{{os_project_name}}.{{domain}}"
        DNS_RECORD_NAME: "vts-exporter"
        DNS_SRV_RECORD: "1 1 443 {{inventory_hostname_short}}"
      delegate_to: 127.0.0.1
      become: false
      when: dc_id is defined and dc_id==2
      ignore_errors: true
    - name: Add vts-exporter dns srv records for Crock Openstack
      script: scripts/ipa_dns_record_add.py
      environment:
        IPA_ENDPOINT: "{{ _ipa_host }}"
        IPA_USER: "{{ _ipa_user.user_input | default(lookup('env','IPA_USER')) }}"
        IPA_PASS: "{{ _ipa_pass.user_input | default(lookup('env','IPA_PASS')) }}"
        DNS_ZONE_NAME: "{{os_project_name}}.{{monitoring_discovery_domain | default ('b-pl.cloud')}}"
        DNS_RECORD_NAME: "vts-exporter"
        DNS_SRV_RECORD: "1 1 443 {{inventory_hostname_short}}"
      delegate_to: 127.0.0.1
      become: false
      when: dc_id is defined and dc_id==1
      ignore_errors: true

  when: custom_nginx is defined and custom_nginx |default('false')|bool

# add dns record for blackbox exporter
- name: Add blackbox-exporter dns srv records Yandex Cloud
  script: scripts/ipa_dns_record_add.py
  environment:
    IPA_ENDPOINT: "{{ _ipa_host }}"
    IPA_USER: "{{ _ipa_user.user_input | default(lookup('env','IPA_USER')) }}"
    IPA_PASS: "{{ _ipa_pass.user_input | default(lookup('env','IPA_PASS')) }}"
    DNS_ZONE_NAME: "{{os_project_name}}.{{domain}}"
    DNS_RECORD_NAME: "blackbox-exporter"
    DNS_SRV_RECORD: "1 1 443 {{inventory_hostname_short}}"
  delegate_to: 127.0.0.1
  become: false
  when: dc_id is defined and dc_id==2
  ignore_errors: true
- name: Add blackbox-exporter dns srv records for Crock Openstack
  script: scripts/ipa_dns_record_add.py
  environment:
    IPA_ENDPOINT: "{{ _ipa_host }}"
    IPA_USER: "{{ _ipa_user.user_input | default(lookup('env','IPA_USER')) }}"
    IPA_PASS: "{{ _ipa_pass.user_input | default(lookup('env','IPA_PASS')) }}"
    DNS_ZONE_NAME: "{{os_project_name}}.{{monitoring_discovery_domain | default ('b-pl.cloud')}}"
    DNS_RECORD_NAME: "blackbox-exporter"
    DNS_SRV_RECORD: "1 1 443 {{inventory_hostname_short}}"
  delegate_to: 127.0.0.1
  become: false
  when: dc_id is defined and dc_id==1
  ignore_errors: true

```

- 01:56:20 - о том как можно разворачивать кластер Kuerneted
  - включен рыбак
  - включен нетворк полиси
  - секюрити контекст
  - лимты
  - горзонтал под автоскеллер (добавляет поды)
  - вертикал автоскеллер (который ноды добавлякт)

- 02:02:10 - самый правильный вариант для разных облаков
  - Terraform мы создаем голую ВМ. Без инициализацй, провижионнга пользователей и всего остального.
  - Terraform создаем ресурсы, сети, балансровщики и т.д.
  - Packer для созданя образов и загрузки их в облако.  эти образы мы начнем использовать. Лучше использовать свои образы.
  - Ansible спиливаем дефолтных пользователей, se-linux  прочее настраиваем  с помощью Ansible
  - в модулях можно описать конфиги для разных облаков. Есл мы едем в это облако, то спользуем эту папку, если в другое облако, то другую папку.
- 02:03: 05 - про утилиту terregrunt - утилита wrapper для Terraform. Позволяет некоторые вещи делать более унверсальными.
#### 


### 47Домашнее задание
Давайте посмотрим ваше домашнее задание.
● Вопросы по домашней работе задавайте в чате мессенджера
Slack.
● Задачи можно сдавать по частям.
● Зачёт по домашней работе проставляется после того, как
приняты все задачи.

### 48Задавайте вопросы и
пишите отзыв о лекции!
Сергей Андрюнин
Сергей Андрюнин
