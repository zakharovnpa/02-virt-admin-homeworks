# 7.2. Облачные провайдеры и синтаксис Terraform." - Захаров Сергей Николаевич

Зачастую разбираться в новых инструментах гораздо интересней понимая то, как они работают изнутри. 
Поэтому в рамках первого *необязательного* задания предлагается завести свою учетную запись в AWS (Amazon Web Services) или Yandex.Cloud.
Идеально будет познакомится с обоими облаками, потому что они отличаются. 

## Задача 1 (вариант с AWS). Регистрация в aws и знакомство с основами (необязательно, но крайне желательно).

Остальные задания можно будет выполнять и без этого аккаунта, но с ним можно будет увидеть полный цикл процессов. 

AWS предоставляет достаточно много бесплатных ресурсов в первых год после регистрации, подробно описано [здесь](https://aws.amazon.com/free/).
1. Создайте аккаунт aws.
1. Установите c aws-cli https://aws.amazon.com/cli/.
1. Выполните первичную настройку aws-sli https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html.
1. Создайте IAM политику для терраформа c правами
    * AmazonEC2FullAccess
    * AmazonS3FullAccess
    * AmazonDynamoDBFullAccess
    * AmazonRDSFullAccess
    * CloudWatchFullAccess
    * IAMFullAccess
1. Добавьте переменные окружения 
    ```
    export AWS_ACCESS_KEY_ID=(your access key id)
    export AWS_SECRET_ACCESS_KEY=(your secret access key)
    ```
1. Создайте, остановите и удалите ec2 инстанс (любой с пометкой `free tier`) через веб интерфейс. 

В виде результата задания приложите вывод команды `aws configure list`.

## Задача 1 (Вариант с Yandex.Cloud). Регистрация в aws и знакомство с основами (необязательно, но крайне желательно).

1. Подробная инструкция на русском языке содержится [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
2. Обратите внимание на период бесплатного использования после регистрации аккаунта. 
3. Используйте раздел "Подготовьте облако к работе" для регистрации аккаунта. Далее раздел "Настройте провайдер" для подготовки
базового терраформ конфига.
4. Воспользуйтесь [инструкцией](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs) на сайте терраформа, что бы 
не указывать авторизационный токен в коде, а терраформ провайдер брал его из переменных окружений.

## Задача 2. Созданием aws ec2 или yandex_compute_instance через терраформ. 

1. В каталоге `terraform` вашего основного репозитория, который был создан в начале курсе, создайте файл `main.tf` и `versions.tf`.
2. Зарегистрируйте провайдер 
   1. для [aws](https://registry.terraform.io/providers/hashicorp/aws/latest/docs). В файл `main.tf` добавьте
   блок `provider`, а в `versions.tf` блок `terraform` с вложенным блоком `required_providers`. Укажите любой выбранный вами регион 
   внутри блока `provider`.
   2. либо для [yandex.cloud](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs). Подробную инструкцию можно найти 
   [здесь](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart).
3. Внимание! В гит репозиторий нельзя пушить ваши личные ключи доступа к аккаунту. Поэтому в предыдущем задании мы указывали
их в виде переменных окружения. 
4. В файле `main.tf` воспользуйтесь блоком `data "aws_ami` для поиска ami образа последнего Ubuntu.  
5. В файле `main.tf` создайте рессурс 
   1. либо [ec2 instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance).
   Постарайтесь указать как можно больше параметров для его определения. Минимальный набор параметров указан в первом блоке 
   `Example Usage`, но желательно, указать большее количество параметров.
   2. либо [yandex_compute_image](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/compute_image).
6. Также в случае использования aws:
   1. Добавьте data-блоки `aws_caller_identity` и `aws_region`.
   2. В файл `outputs.tf` поместить блоки `output` с данными об используемых в данный момент: 
       * AWS account ID,
       * AWS user ID,
       * AWS регион, который используется в данный момент, 
       * Приватный IP ec2 инстансы,
       * Идентификатор подсети в которой создан инстанс.  
7. Если вы выполнили первый пункт, то добейтесь того, что бы команда `terraform plan` выполнялась без ошибок. 

**Ответ:**

Листинг команды ` terraform plan ` в Yandex.Cloud

```hcl
root@PC-Ubuntu:~/netology-project/learning-terraform/yandex-cloud-learning# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node01"
      + network_acceleration_type = "standard"
      + platform_id               = "standard-v1"
      + service_account_id        = (known after apply)
      + status                    = (known after apply)
      + zone                      = "ru-central1-a"

      + boot_disk {
          + auto_delete = true
          + device_name = (known after apply)
          + disk_id     = (known after apply)
          + mode        = (known after apply)

          + initialize_params {
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node01"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.11"
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = (known after apply)
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_vpc_network.default will be created
  + resource "yandex_vpc_network" "default" {
      + created_at                = (known after apply)
      + default_security_group_id = (known after apply)
      + folder_id                 = (known after apply)
      + id                        = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_vm_1 = (known after apply)
  + internal_ip_address_vm_1 = "192.168.101.11"

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.

   
```


В качестве результата задания предоставьте:
1. Ответ на вопрос: при помощи какого инструмента (из разобранных на прошлом занятии) можно создать свой образ ami?
 **Ответ:** Свой образ AMI (Amazon Mashine Images) можно создать с помощью таких инструментов, как специализированного CloudFormation и универсального Terraform.
   1. AWS CloudFormation предлагает простой способ моделирования наборов связанных ресурсов AWS и сторонних ресурсов, их быстрого и единообразного выделения, а также управления ими на протяжении всего жизненного цикла за счет работы с инфраструктурой как с кодом. Шаблон CloudFormation описывает требуемые ресурсы и их зависимости, что позволяет запускать и настраивать их вместе в виде стека. Вместо того чтобы управлять ресурсами по отдельности, можно использовать шаблон для создания, обновления и удаления всего стека как единого целого. Управлять стеками и выделять их можно в нескольких аккаунтах и регионах AWS.
   CloudFormation позволяет моделировать всю облачную инфраструктуру в текстовых файлах. Для описания ресурсов AWS, которые нужно создать и настроить, можно использовать декларативные языки с открытым кодом, например JSON или YAML. В инструменте AWS CloudFormation Designer реализовано визуальное проектирование, что поможет начать работу с шаблонами AWS CloudFormation.
   При управлении стеком AWS CloudFormation автоматически контролирует зависимости между ресурсами. Нет необходимости указывать определенный порядок создания, обновления и удаления ресурсов; при выполнении операций со стеками CloudFormation самостоятельно определяет последовательность действий для каждого ресурса. 
   Источник: сайт [AWS CloudFormation](https://aws.amazon.com/ru/cloudformation/features/)
   
   2. Terraform — программное обеспечение с открытым исходным кодом, созданное компанией HashiCorp. Пользователи определяют и предоставляют инфраструктуру центра обработки данных с помощью декларативного языка конфигурации, известного как HashiCorp Configuration Language (HCL) или JSON.
Terraform управляет внешними ресурсами (такими как инфраструктура общедоступного облака, инфраструктура частного облака, сетевые устройства, программное обеспечение как услуга и платформа как услуга) с «поставщиками». HashiCorp поддерживает обширный список официальных поставщиков, а также может интегрироваться с поставщиками, разработанными сообществом. Пользователи могут взаимодействовать с поставщиками Terraform, объявляя ресурсы или вызывая источники данных. Вместо того, чтобы использовать императивные команды для предоставления ресурсов, Terraform использует декларативную конфигурацию для описания желаемого конечного состояния. Как только пользователь вызывает Terraform для данного ресурса, Terraform будет выполнять действия CRUD от имени пользователя для достижения желаемого состояния. Инфраструктура как код может быть написана в виде модулей, что обеспечивает возможность повторного использования и поддержку кода.
Terraform поддерживает ряд поставщиков облачной инфраструктуры, таких как Amazon Web Services, Microsoft Azure, IBM Cloud, Google Cloud Platform, DigitalOcean, Oracle Cloud, Yandex.Cloud, VMware vSphere и OpenStack.
Источник: сайт [wikipedia.org](https://ru.wikipedia.org/wiki/Terraform)
   
3. Ссылку на репозиторий с исходной конфигурацией терраформа.  
 
---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

