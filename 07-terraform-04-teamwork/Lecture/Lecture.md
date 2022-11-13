### Лекция по теме "Средства командной работы"

- 00:07:05 - доработал модули Yandex
- 00:07:23 - в Yandex.Cloud через ресурс менеджер можно создать папки (для автоматзаци задач создания ресурсов с Terraform) и получить ее ID этой папки. 
- 00:07:40 - в провайдере Yandex для Terraform это все находилось не в VPC, а в отдельном месте. Для динамческого созданя ресурсов в Яндексе. Прмеры лежать здесь: [Terraform](https://gitlab.com/k11s-os/infrastructure-as-code/-/tree/main/) 
- 00:11:15 - про Ansible Tower (бесплатный)  и Ansible OWX (платный) - для сохраненя выхлопа, когда работает Ansible
- 00:11:50 - для Terraform тоже есть возможность сохранить выхлоп
- 00:12:00 - про технологию работы с PR (pooll request). Есть ветка main, в которую запрещены коммиты. У нас есть gitflow. Мы отпочковываемся в новую ветку, делаем там изменения и коммиты, затем создаем PR (pooll request). Мы можем посмотреть что у нас там применится и если этот PR (pooll request) аппрувят, то мы применяем изменения на инфраструктуру. Для этого мержим в ветку мастер. Таким образом все наши измененя идут из ветки мастер.
- 

Сергей
Андрюнин
#### Средства командной работы
2
Сергей Андрюнин
DevOps-инженер
RTLabs
1. Средства командной работы
2. Terraform cloud
3. Атлантис
4. Remote state
5. Модули
6. Домашнее задание
План занятия
3

#### Средства командной работы
4

#### Основные инструменты
5
● Terraform Cloud / Terraform Enterprise
○ Есть бесплатные тарифы, но полный функционал платный.
○ Хостится на сервера hashicorp.
● Atlantis
○ Решение с открытым исходным кодом.
○ Запускается на ваших серверах.

#### Зачем использовать эти инструменты?
6
● Прозрачность процессов
○ Если каждый запускает локально – не понятно что сейчас
задеплоено.
○ Кто-то мог забыть закоммитить изменения.
○ Есть логи всех plan и apply.

### Каждый может сделать PR в инфраструктуру
7
● Каждый может сделать PR и посмотреть plan своих изменений.
○ Это существенно ускоряет процессы: вместо того чтобы
ставить задачу на простое изменение, разработчик просто
делает PR.
● Все секретные данные будут скрыты в пределах этой системы.

### Более качественный процесс ревью PR
8
● Можно проверить код.
● Сразу виден результат работы terraform plan.

### Стандартизация рабочих процессов
9
● Система блокирует рабочее пространство (workspace) до
применения изменений или ручного снятия блокировки.
● Помимо стандартных команд plan и apply можно добавить
дополнительные инструкции.

### Terraform Cloud
### Terraform Cloud
Поддерживает несколько типов:
● На основе системы контроля версий,
● Просто remote backend запускаемый вручную,
● На основе API (много возможностей, но сложно использовать). - 00:16:10 для создания ресурсов через веб-интерфейс

### Terraform Cloud
Особенности:
● Поддерживаем remote state.
● Необходимо обеспечить доступ к api своих сервисов.
● Поддерживается командой терраформа.
● Есть бесплатный тарифный план.
● Хороший UI с возможностью ревью изменений.
● Интеграция с slack.
● Можно задавать переменные для разных окружений.

### Атлантис
### Автоматизация pull request
16
Сайт: https://www.runatlantis.io/
Совместимо с:
● GitHub
● GitLab
● Bitbucket
● Azure DevOps

### Особенности
17
● Бесплатное решение.
● Поддерживает множество популярных хранилищ
репозиториев.
● Достаточно где угодно запустить докер контейнер с набором
переменных окружения

### Шаг 1
18
Открывает pull request в репозитории с кодом terraform

### Шаг 2
19
Атлантис
автоматически
запускает terraform
plan и оставляет
комментарий к PR.

### Шаг 3
20
Кто-то из вашей команды просматривает план и одобряет PR

### Шаг 4
21
Вы оставляете комментарий atlantis apply

### Шаг 5
22
Атлантис исполняет terraform apply и оставляет комментарий об этом

### Шаг 6
23
Атлантис автоматически мержит PR

### Настройка сервера
24
Давайте посмотрим пример конфига:
https://www.runatlantis.io/docs/server-side-repo-config.html
● Проверка апрува PR.
● Проверка "Mergeable" статуса.
● Разрешения изменять настройки внутри репозитория.
● Изменения стандартного воркфлоу атлантиса.

- 00:25:40 - описание пирмера настройки серверного конфига, показаны workflow_hooks,  шаги workflow

### Настройка клиента
25
Давайте посмотрим пример конфига:
https://www.runatlantis.io/docs/repo-level-atlantis-yaml.html
● Настройка авто планирования.
● Триггеры авто планирования.
● Установка конкретной версии терраформа.
● Разные воркспейсы.
● Апрув для конкретных воркспейсов.

- 00:27:40 - описание пирмера настройки клиентского конфига,


### Remote state

### Чтение удаленного состояния проекта  - 00:29:20
27
Получает данные об удаленном состоянии проекта
Terraform.
Это позволяет использовать outputs параметры одного
проекта в качестве входных данных для других проектов.

- 00:29:20 - !!! про Remote state (удаленное состояние). файлы `tf.state` описывают удаленное состояне текущей иинфраструктцры и перед тем, как сделать изменения терраформ забирает удаленное состояние, сравнивает его и показывает в итоге измененный выхлоп. Это позволяет использовать outputs параметры одного проекта в качестве входных данных для других проектов. Можно разбить наш проект на несколько мелких частей. На пример Core Team - основная команда, которая занимается только облаком. Иногда их называют Shared ITб инфраструктурщки. Они подготовили VPC, выдали на нее права и могут дать возможность чтать некоторые переменные


### Пример remote_state - 00:32:20
28
```tf
data "terraform_remote_state" "vpc" {
backend = "remote"
config = {
organization = "hashicorp"
workspaces = {
name = "vpc-prod"
}
}
}
resource "aws_instance" "foo" {
# ...
subnet_id = data.terraform_remote_state.vpc.outputs.subnet_id
```
- 00:33:00 - вы создали VPC и чтобы раздать ID на всё, чтобы разработчк мог сам собирать  разбрать ВМ для него нужны ID облака, подсети, папки, и др. 
Мы говорим разрабу как это все можно забрать и он забрает их  все отлично. 


### Модули

- 00:33:00 - про модули Terraform. Это аналог подключаемых бибилиотек в программах или ЯП.Это код на HCL для Terraform, который опсывает какой-то ресурс. Можно не писать тонну кода, а взять 5 строк и у нас все заведется. Используя модули от провайдера мы не беспокомся об изменениях, которые могут быть у провайдера в настройках. Все идет вместе в модулем. Вместо того, чтобы писать много кода, мы подключаем модуль и все там делается под капотом

- [Private bucket with versioning enabled](https://github.com/terraform-aws-modules/terraform-aws-s3-bucket#private-bucket-with-versioning-enabled)

- 00:37:00 - !!! про модуль VPC. Создан преподавателем Андрюниным. Есть прмер файла `main.tf` , `varibales.tf` для автоматического созданя VPC
- 00:39:00 - про создание папок для модулей Terraform
- 00:40:00 - показаны переменные для разных workspace - prod, stage. На выхлопе он получит ID папки, ее название и адрес подсети.
- Модуль [hamnsk/vpc](https://registry.terraform.io/modules/hamnsk/vpc/yandex/latest) - описание модуля на 00:39:16
- main.tf
```tf
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
      version = "0.61.0"
    }
  }
}


# Provider
provider "yandex" {
  token     = var.yc_token
  cloud_id  = var.yc_cloud_id
  zone      = var.yc_region
}

module "vpc" {
  source  = "hamnsk/vpc/yandex"
  version = "0.5.0"
  description = "managed by terraform"
  create_folder = length(var.yc_folder_id) > 0 ? false : true  # Создане папок для модулей Terraform
  yc_folder_id = var.yc_folder_id
  name = terraform.workspace
  subnets = local.vpc_subnets[terraform.workspace]
}

locals {
  vpc_subnets = {
    default = [
      {
        "v4_cidr_blocks": [
          "10.128.0.0/24"
        ],
        "zone": var.yc_region
      }
    ]
    stage = [
      {
        "v4_cidr_blocks": [
          "10.128.0.0/24"
        ],
        "zone": var.yc_region
      }
    ]
    prod = [
      {
        zone           = "ru-central1-a"
        v4_cidr_blocks = ["10.128.0.0/24"]
      },
      {
        zone           = "ru-central1-b"
        v4_cidr_blocks = ["10.129.0.0/24"]
      },
      {
        zone           = "ru-central1-c"
        v4_cidr_blocks = ["10.130.0.0/24"]
      }
    ]
  }
}

```

- variables.tf
```tf
variable "yc_token" {
   default = ""
}

variable "yc_cloud_id" {
  default = ""
}

variable "yc_folder_id" {
  default = ""
}

variable "yc_region" {
  default = "ru-central1-a"
}


```

### Рекомендации - 00:41:40
30
● Старайтесь держать модули простыми.
● Иногда есть смысл использовать отдельный проект с
remote_state, а не отдельный модуль.
● Используйте сторонние модули предварительно изучив их.

- 00:41:40

### Каталог модулей
31
● Основные провайдеры имеют наборы готовых модулей.
● Основной каталог модулей:
https://registry.terraform.io/browse/modules.

### Итого
Что мы разобрали:
● Средства для организации командной работы.
● Как организовывать свои модули и связи между проектами.
● Как пользоваться существующими модулями.

- [Здесь тоже прмеры ](https://gitlab.com/k11s-os/infrastructure-as-code/-/blob/main/terraform/demo/vars.tf)

### Дополнительные матералы
- 00:46:00 - как создавать workspace на сайте app.terraform.io
### Пример файла instance.tf - 00:48:16 
- instance.tf [Пример отсюда](https://gitlab.com/k11s-os/infrastructure-as-code/-/blob/main/terraform/modules/instance/instance.tf)
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



- 00:49:00 - показан файл main.tf с настройкам
- main.tf Пример отсюда
```tf
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
      version = "0.61.0"
    }
  }
}


# Provider
provider "yandex" {
  token     = var.yc_token
  cloud_id  = var.yc_cloud_id
  zone      = var.yc_region
}

module "vpc" {
  source  = "hamnsk/vpc/yandex"
  version = "0.5.0"
  description = "managed by terraform"
  create_folder = length(var.yc_folder_id) > 0 ? false : true  # Создане папок для модулей Terraform
  yc_folder_id = var.yc_folder_id
  name = terraform.workspace
  subnets = local.vpc_subnets[terraform.workspace]
}

locals {
  news_cores = {
    default = 2
    stage = 2
    prod = 2
  }
  news_disk_size = {
    default = 20
    stage = 20
    prod = 40
  }
  news_instance_count = {
    default = 1
    stage = 1
    prod = 2
  }
  vpc_subnets = {
    default = [
      {
        "v4_cidr_blocks": [
          "10.128.0.0/24"
        ],
        "zone": var.yc_region
      }
    ]
    stage = [
      {
        "v4_cidr_blocks": [
          "10.128.0.0/24"
        ],
        "zone": var.yc_region
      }
    ]
    prod = [
      {
        zone           = "ru-central1-a"
        v4_cidr_blocks = ["10.128.0.0/24"]
      },
      {
        zone           = "ru-central1-b"
        v4_cidr_blocks = ["10.129.0.0/24"]
      },
      {
        zone           = "ru-central1-c"
        v4_cidr_blocks = ["10.130.0.0/24"]
      }
    ]
  }
}
```

- 00:50:40 - настройки ВМ
- 00:50:55 - запуск созданя ресурсов на основе файла main.tf
- 00:51:20 - terraform workspace show
- 00:52:59 - вывод terraform plan
- создаем днамически папку
- параметры создания инстанса
- 00:53:30 - terraform apply
- 00:55:00 - как передать folder_id в переменные
- 00:56:20 - terraform workspace select prod
- 00:57:20 - исправление ошибки
- 00:59:40 - после исправленя ошибки

### Пример того, как надо делать на проекте
1. Хранить весь код в Гите вместе с состоянием и все на свете
2. Катить только рукам. ??? на 01:04:10 - про оборачивание Terraform  в Playbook
3. Когда начинаем что-то катить, то в общем рабочем чате предупреждал, что сейчас будут накатываться зменения. 
4. Закрыть задачу 
5. Просьба всех сделать git pool


### Домашнее задание - 01:95:00
Давайте посмотрим ваше домашнее задание.
● Вопросы по домашней работе задавайте в чате мессенджера .
● Задачи можно сдавать по частям.
● Зачёт по домашней работе проставляется после того, как приняты
все задачи

### Ответы на вопросы - 01:08:50
- 01:11:20 - по Dockerfile Redis. Здесь поднимается стек который с метрками, с мониторнгом, [Redis](https://github.com/hamnsk/go_psql_redis_example)
```sh
FROM golang:1.17.1-alpine3.14 AS builder

WORKDIR /usr/local/go/src/

COPY ./app/ /usr/local/go/src/

RUN go clean --modcache
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -mod=readonly -o redis-cache cmd/redis-cache-example/main.go

FROM scratch
ENV DATABASE_URL=db
ENV REDIS=redis
ENV SENTRY_DSN=dsn
WORKDIR /app
COPY --from=builder /usr/local/go/src/redis-cache /app/
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

CMD ["/app/redis-cache"]
```
- 01:11:12 - про Kubespray. Создан на основе Kubeadm. 
- Для изучения того как устанаввать Kubernetes надо его рукам установить с помощью Kubeadm
- 01:16:45 - о системе логов , трейсов и псать их куда угодно. [Vector](https://github.com/vectordotdev/vector)
- 01:17:40 - про Memcashed вычисленя. Лучше использовать Redis
