# "7.3. Основы и принцип работы Терраформ" -  Захаров Сергей Николаевич

## Задача 1. Создадим бэкэнд в S3 (необязательно, но крайне желательно).

Если в рамках предыдущего задания у вас уже есть аккаунт AWS, то давайте продолжим знакомство со взаимодействием
терраформа и aws. 

1. Создайте s3 бакет, iam роль и пользователя от которого будет работать терраформ. Можно создать отдельного пользователя,
а можно использовать созданного в рамках предыдущего задания, просто добавьте ему необходимы права, как описано 
[здесь](https://www.terraform.io/docs/backends/types/s3.html).
1. Зарегистрируйте бэкэнд в терраформ проекте как описано по ссылке выше. 

**Ответ:**

## Задача 2. Инициализируем проект и создаем воркспейсы. 

1. Выполните `terraform init`:
    * если был создан бэкэнд в S3, то терраформ создат файл стейтов в S3 и запись в таблице 
dynamodb.
    * иначе будет создан локальный файл со стейтами.  
1. Создайте два воркспейса `stage` и `prod`.
1. В уже созданный `aws_instance` добавьте зависимость типа инстанса от воркспейса, чтобы в разных ворскспейсах 
использовались разные `instance_type`.
1. Добавим `count`. Для `stage` должен создаться один экземпляр `ec2`, а для `prod` два. 
1. Создайте рядом еще один `aws_instance`, но теперь определите их количество при помощи `for_each`, а не `count`.
1. Что бы при изменении типа инстанса не возникло ситуации, когда не будет ни одного инстанса добавьте параметр
жизненного цикла `create_before_destroy = true` в один из ресурсов `aws_instance`.
1. При желании поэкспериментируйте с другими параметрами и ресурсами.

В виде результата работы пришлите:
* Вывод команды `terraform workspace list`.
* Вывод команды `terraform plan` для воркспейса `prod`.  

**Ответ:**

1. Задание не выполнено, т.к. УЗ на AWS отсутствует.
2. Создайте два воркспейса `stage` и `prod`.

![terraform-workspace-list](/)
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform workspace new stage
Created and switched to workspace "stage"!

You're now on a new, empty workspace. Workspaces isolate their state,
so if you run "terraform plan" Terraform will not see any existing state
for this configuration.
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform workspace new prod
Created and switched to workspace "prod"!

You're now on a new, empty workspace. Workspaces isolate their state,
so if you run "terraform plan" Terraform will not see any existing state
for this configuration.
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform workspace list
  default
* prod
  stage

```
3. В уже созданный `aws_instance` добавим зависимость типа инстанса от воркспейса, чтобы в разных ворскспейсах 
использовались разные `instance_type`.

Добавлен блок
```ps
locals {
	instance_type_map = {
		stage = "t3.micro"
		prod = "t3.large"
	}
}

```
4. Добавим параметр `count`, определяющий кол-во создаваемых ВМ в каждом воркспейсе. Для воркспейс `stage` должен создаться один экземпляр `ec2`, а для `prod` два экземпляра. 

```ps
resource "aws_instance" "web" {
	ami = data.aws_ami.amazon_linux.id 
	instance_type = "t3.micro"
	count = local.instance_count_map[terraform.workspace]}


locals {
	instance_count_map = {
	stage = 1
	prod = 2
	}
}

```
5. Создаем рядом еще один `aws_instance`, но теперь их количество определим при помощи `for_each`, а не `count`.
```ps
resource "aws_instance" "web" {
	for_each = local.instances 
	ami = each.value
	instance_type = each.key
}


locals {
	instances = {
		"t3.micro" = data.aws_ami.amazon_linux.id   
		"t3.large" = data.aws_ami.amazon_linux.id
	}
}

```
6. Что бы при изменении типа инстанса не возникло ситуации, когда не будет ни одного инстанса добавим параметр
жизненного цикла `create_before_destroy = true` в один из ресурсов `aws_instance`.
```ps
resource "aws_instance" "web" {
	ami = data.aws_ami.amazon_linux.id 
	instance_type = "t3.micro"
	tags = {"project": "main"
}
	
lifecycle {
	create_before_destroy = true   
#	prevent_destroy = true
#	ignore_changes = ["tags"] 
	}
}
```
7. Вывод команды `terraform workspace list`.
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform workspace list
  default
* prod
  stage

```
9. Вывод команды `terraform plan` для воркспейса `prod`.
```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform workspace show
prod
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.web[0] will be created
  + resource "aws_instance" "web" {
      + ami                          = "ami-0c55b159cbfafe1f0"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t3.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

  # aws_instance.web[1] will be created
  + resource "aws_instance" "web" {
      + ami                          = "ami-0c55b159cbfafe1f0"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t3.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.

```

---
