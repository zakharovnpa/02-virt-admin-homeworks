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
```python
resource "aws_vpc" "main" {
      cidr_block = var.base_cidr_block
}

тип "идентификатор" "имя" {
      название_параметра = выражение_значение_параметра
}
```
### 30Блок провайдеров
registry.terraform.io/providers/hashicorp/aws/latest/docs
```python
provider "aws" {
    region = "us-east-1"
}
```
### 31Блок требований к провайдерам
Блок «terraform» для указаний версий провайдеров и бэкэндов.
```python
terraform {
    required_providers {
        aws = {
            source = "hashicorp/aws"
            version = "~> 3.0"
    }
  }
}
```
### 32Блок ресурсов
registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance
Ресурс **aws_instance** – это экземпляр ec2
```python
resource "aws_instance" "web" {
   ami = data.aws_ami.ubuntu.id
      instance_type = "t3.micro"
}
```
### 33Блок внешних данных
Для того что бы прочитать данные из внешнего API и использовать для создания других рессурсов.
Use this data source to get the access to the effective Account ID, User ID, and ARN in which Terraform is authorized.
[Data Source: aws_caller_identity](registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)
```python
data "aws_caller_identity" "current" {}

// data.aws_caller_identity.current.account_id
// data.aws_caller_identity.current.arn
// data.aws_caller_identity.current.user_id
```
### 34Блок переменных
Каждый модуль может зависеть от переменных.
```python
variable "image_id" {
    type = string
}

resource "aws_instance" "example" {
      instance_type = "t2.micro"
      ami           = var.image_id
}
```
### 35Блок переменных
Структура переменной может быть достаточно сложной.
```bash
variable "availability_zone_names" {
type
= list(string)
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
### 36Типы переменных
Примитивные типы:
```
●
string
● number
● bool
Комбинированные типы:
● list(<TYPE>)
● set(<TYPE>)
● map(<TYPE>)
● object({<ATTR NAME> = <TYPE>, ... })
● tuple([<TYPE>, ...])
  ```

### 37Валидация переменных
```bash
Особенно важно для повторно используемых модулей.
variable "image_id" {
type
= string
description = "The id of the machine image (AMI) to use
for the server."
validation {
condition
= length(var.image_id) > 4 &&
substr(var.image_id, 0, 4) == "ami-"
error_message = "The image_id value must be a valid AMI
id, starting with \"ami-\"."
}
}
```
### 38Блок output
Для того чтобы разные модули могли использовать результат
работы друг друга.
```bash
output "instance_ip_addr" {
    value = aws_instance.server.private_ip
    description = "The private IP address of the main server instance."

depends_on = [

# Security group rule должна быть создана перед тем как
можно будет использовать этот ip адрес, иначе сервис будет
недоступен
    aws_security_group_rule.local_access,
  ]
}
```
### 39Локальные переменные
Могут быть использованы внутри модуля сколько угодно раз.
```bash
locals {
    service_name = "forum"
    owner         = "Community Team"
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

### 40Комментарии
Terraform поддерживает несколько видов комментариев:
```bash
# начинает однострочные комментарии;
// также однострочные комментарии;
/* и */ для обозначения многострочных комментариев.
```

### 41Структура проекта

### 42Структура каталогов
- /main.tf
- /any_ﬁle.tf
- /modules/
- /modules/awesome_module/
- /modules/awesome_module/main.tf
- /modules/awesome_module/any_other_ﬁle.tf
- /modules/next_module/
- /modules/next_module/main.tf
- /modules/next_module/any_other_ﬁle.tf

### 43Структура файлов
- main.tf
- variables.tf
- outputs.tf
- any_other_ﬁles.tf

### 44Итоги

### 45Итоги
Сегодня мы:
- Познакомились с облачными провайдерами AWS и Yandex.Cloud$
- Познакомились с базовым синтаксисом Terraform;
- Узнали, как создавать виртуальный инстанс ec2:
  - через веб интерфейс,через cli консоль,
  - при помощи Terraform.

### 46Домашнее задание

https://gitlab.com/k11s-os


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
