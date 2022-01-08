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

```

---
