### Синтаксис Terraform. 31:18

### 27Terraform
Terraform – это просто API-клиент. Это бинарник, написанный на языке GO от компании Hashicorp.
Это синтаксический анализатор кода на языке HCL. Скоро будет HCL2.
Террафрм осуществляет свои действия с помощью провайдеров.
Terraform-провайдеры «знают» все эти команды и умеют приводить состояние ресурсов к описанному в своих конфигурационных файлах.
Провайдеры могут работать как с любым клиентом: cli, http, их комбинациями и другими.

### 28Terraform-провайдеры
terraform.io/docs/providers/index.html
В официальном репозитории около 150 штук. Плюс много неофициальных, и можно достаточно просто создавать собственные.

### Блок провайдеров
registry.terraform.io/providers/hashicorp/aws/latest/docs

### Блок ресурсов
registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance

### 33Блок внешних данных
Для того что бы прочитать данные из внешнего API и использовать для создания других рессурсов.
Use this data source to get the access to the effective Account ID, User ID, and ARN in which Terraform is authorized.
[Data Source: aws_caller_identity](registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity)



### 29Блоки
Все конфигурации описываются в виде блоков. Например:
```python
resource "aws_vpc" "main" {
      cidr_block = var.base_cidr_block
}

тип "идентификатор" "имя" {
      название_параметра = выражение_значение_параметра
}
```

```hcl
# Блок провайдеров
provider "aws" {
    region = "us-east-1"
}

#   Блок требований к провайдерам
# Блок «terraform» для указаний версий провайдеров и бэкэндов.
terraform {
    required_providers {
        aws = {
            source = "hashicorp/aws"
            version = "~> 3.0"
    }
  }
}

# Блок ресурсов. Ресурс **aws_instance** – это экземпляр ec2
resource "aws_instance" "web" {
   ami = data.aws_ami.ubuntu.id
      instance_type = "t3.micro"
}

# Блок внешних данных. Для того что бы прочитать данные из внешнего API и использовать для создания других рессурсов.
data "aws_caller_identity" "current" {} # Так вернется под какой УЗ мы сейчас препарируем облако

// data.aws_caller_identity.current.account_id
// data.aws_caller_identity.current.arn
// data.aws_caller_identity.current.user_id
```
### Блок переменных
Каждый модуль может зависеть от переменных.
```hcl
variable "image_id" {
    type = string
}

resource "aws_instance" "example" {
      instance_type = "t2.micro"
      ami           = var.image_id  # Чтобы обратиться к переменной пишем "var."
}
```
### Блок переменных
Структура переменной может быть достаточно сложной.
```hcl
variable "availability_zone_names" {
    type    = list(string)
    default = ["us-west-1a"]
}
variable "docker_ports" {
    type     = list(object({
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
### Типы переменных
Примитивные типы:
```hcl
● string
● number
● bool
```
Комбинированные типы:
```hcl
● list(<TYPE>)
● set(<TYPE>)
● map(<TYPE>)
● object({<ATTR NAME> = <TYPE>, ... })
● tuple([<TYPE>, ...])
```

### Валидация переменных
Особенно важно для повторно используемых модулей.
```hcl
variable "image_id" {
    type        = string
    description = "The id of the machine image (AMI) to use for the server."
validation {
    condition = length(var.image_id) > 4 &&
    substr(var.image_id, 0, 4) == "ami-"
    
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```
### Блок output
Для того чтобы разные модули могли использовать результат работы друг друга.
```hcl
output "instance_ip_addr" {
    value = aws_instance.server.private_ip
    description = "The private IP address of the main server instance."

depends_on = [

# Security group rule должна быть создана перед тем как
# можно будет использовать этот ip адрес, иначе сервис будет
# недоступен
    aws_security_group_rule.local_access,
  ]
}
```
### Локальные переменные
Могут быть использованы внутри модуля сколько угодно раз.
```hcl
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
```hcl
# начинает однострочные комментарии;

// также однострочные комментарии;

/* и 
для обозначения 
многострочных 
комментариев.
*/ 

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
