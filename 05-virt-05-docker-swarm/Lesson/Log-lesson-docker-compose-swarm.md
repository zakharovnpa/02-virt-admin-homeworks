# Выполнение задания по теме "Оркестрация кластером Docker контейнеров на примере Docker Swarm" на Sergey-PC, Ubuntu-20.04
## Логи выполнения домашнего задания на физической ОС Ubuntu на Sergey-PC
## Предварительные настройки
1. Создать директорию проекта  ` root@PC-Ubuntu:~/netology-project# mkdir -p Docker-Compose-Swarm `
2. Перенести директорию ` src ` из директории с домашнним заданием

### Задание
1. Авторизуемся в Yandex.Cloud.
2. Создаём сеть и подсеть, чтобы собрать образ ОС с помощью Packer и запускаем сборку образа.
3. Удаляем подсеть и сеть, которую использовали для сборки образа ОС.
4. Создаём 6 виртуальных машин с помощью Terraform.
5. Создаём Docker Swarm кластер из виртуальных машин, созданных на предыдущем шаге.
6. Запускаем деплой стека приложений.
7. Проводим стресс тест Docker Swarm кластера.
8. Удаляем всё, чтобы не тратить деньги!

### Практическая часть
#### 1. Авторизуемся в Yandex.Cloud.
#### 2. Создаём сеть и подсеть, чтобы собрать образ ОС с помощью Packer и запускаем сборку образа.
#### 3. Удаляем подсеть и сеть, которую использовали для сборки образа ОС.
#### 4. Создаём 6 виртуальных машин с помощью Terraform.
- Инициализация terraform
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of yandex-cloud/yandex...
- Finding latest version of hashicorp/null...
- Finding latest version of hashicorp/local...
- Installing yandex-cloud/yandex v0.68.0...
- Installed yandex-cloud/yandex v0.68.0 (self-signed, key ID E40F590B50BB8E40)
- Installing hashicorp/null v3.1.0...
- Installed hashicorp/null v3.1.0 (signed by HashiCorp)
- Installing hashicorp/local v2.1.0...
- Installed hashicorp/local v2.1.0 (signed by HashiCorp)

Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://www.terraform.io/docs/cli/plugins/signing.html

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
```
Проверка готовности terraform
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform validate
╷
│ Error: JSON in "key.json" are not valid: invalid character 'k' looking for beginning of value
│ 
│   with provider["registry.terraform.io/yandex-cloud/yandex"],
│   on provider.tf line 11, in provider "yandex":
│   11:   service_account_key_file = "key.json"
│ 
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
```
Ошибка. Необходимо добавить ключ "key.json" сервисного аккаунта Яндекс.Облака
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# mc

root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform validate
Success! The configuration is valid.

root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
```
Проверяем план работы terraform по созданию ВМ
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.inventory will be created
  + resource "local_file" "inventory" {
      + content              = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "../ansible/inventory"
      + id                   = (known after apply)
    }

  # null_resource.cluster will be created
  + resource "null_resource" "cluster" {
      + id = (known after apply)
    }

  # null_resource.monitoring will be created
  + resource "null_resource" "monitoring" {
      + id = (known after apply)
    }

  # null_resource.sync will be created
  + resource "null_resource" "sync" {
      + id = (known after apply)
    }

  # null_resource.wait will be created
  + resource "null_resource" "wait" {
      + id = (known after apply)
    }

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

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node02"
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
              + name        = "root-node02"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.12"
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

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node03"
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
              + name        = "root-node03"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.13"
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

  # yandex_compute_instance.node04 will be created
  + resource "yandex_compute_instance" "node04" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node04.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node04"
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
              + name        = "root-node04"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.14"
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

  # yandex_compute_instance.node05 will be created
  + resource "yandex_compute_instance" "node05" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node05.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node05"
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
              + name        = "root-node05"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.15"
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

  # yandex_compute_instance.node06 will be created
  + resource "yandex_compute_instance" "node06" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node06.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node06"
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
              + name        = "root-node06"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.16"
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
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 13 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01 = (known after apply)
  + external_ip_address_node02 = (known after apply)
  + external_ip_address_node03 = (known after apply)
  + external_ip_address_node04 = (known after apply)
  + external_ip_address_node05 = (known after apply)
  + external_ip_address_node06 = (known after apply)
  + internal_ip_address_node01 = "192.168.101.11"
  + internal_ip_address_node02 = "192.168.101.12"
  + internal_ip_address_node03 = "192.168.101.13"
  + internal_ip_address_node04 = "192.168.101.14"
  + internal_ip_address_node05 = "192.168.101.15"
  + internal_ip_address_node06 = "192.168.101.16"

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.

```
##### Запуск с ошибкой
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.inventory will be created
  + resource "local_file" "inventory" {
      + content              = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "../ansible/inventory"
      + id                   = (known after apply)
    }

  # null_resource.cluster will be created
  + resource "null_resource" "cluster" {
      + id = (known after apply)
    }

  # null_resource.monitoring will be created
  + resource "null_resource" "monitoring" {
      + id = (known after apply)
    }

  # null_resource.sync will be created
  + resource "null_resource" "sync" {
      + id = (known after apply)
    }

  # null_resource.wait will be created
  + resource "null_resource" "wait" {
      + id = (known after apply)
    }

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

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node02"
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
              + name        = "root-node02"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.12"
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

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node03"
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
              + name        = "root-node03"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.13"
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

  # yandex_compute_instance.node04 will be created
  + resource "yandex_compute_instance" "node04" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node04.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node04"
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
              + name        = "root-node04"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.14"
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

  # yandex_compute_instance.node05 will be created
  + resource "yandex_compute_instance" "node05" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node05.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node05"
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
              + name        = "root-node05"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.15"
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

  # yandex_compute_instance.node06 will be created
  + resource "yandex_compute_instance" "node06" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node06.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node06"
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
              + name        = "root-node06"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.16"
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
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 13 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01 = (known after apply)
  + external_ip_address_node02 = (known after apply)
  + external_ip_address_node03 = (known after apply)
  + external_ip_address_node04 = (known after apply)
  + external_ip_address_node05 = (known after apply)
  + external_ip_address_node06 = (known after apply)
  + internal_ip_address_node01 = "192.168.101.11"
  + internal_ip_address_node02 = "192.168.101.12"
  + internal_ip_address_node03 = "192.168.101.13"
  + internal_ip_address_node04 = "192.168.101.14"
  + internal_ip_address_node05 = "192.168.101.15"
  + internal_ip_address_node06 = "192.168.101.16"
yandex_vpc_network.default: Creating...
yandex_vpc_network.default: Creation complete after 1s [id=enphkubv2mkhbjhs9hs1]
yandex_vpc_subnet.default: Creating...
yandex_vpc_subnet.default: Creation complete after 1s [id=e9b814rva083lct8fq02]
yandex_compute_instance.node01: Creating...
yandex_compute_instance.node02: Creating...
yandex_compute_instance.node06: Creating...
yandex_compute_instance.node04: Creating...
yandex_compute_instance.node03: Creating...
yandex_compute_instance.node05: Creating...
yandex_compute_instance.node06: Still creating... [10s elapsed]
yandex_compute_instance.node02: Still creating... [10s elapsed]
yandex_compute_instance.node03: Still creating... [10s elapsed]
yandex_compute_instance.node04: Still creating... [10s elapsed]
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node05: Still creating... [10s elapsed]
yandex_compute_instance.node06: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node04: Still creating... [20s elapsed]
yandex_compute_instance.node03: Still creating... [20s elapsed]
yandex_compute_instance.node02: Still creating... [20s elapsed]
yandex_compute_instance.node05: Still creating... [20s elapsed]
yandex_compute_instance.node06: Creation complete after 27s [id=fhm66homrnuh7j49td8u]
yandex_compute_instance.node03: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node04: Still creating... [30s elapsed]
yandex_compute_instance.node02: Still creating... [30s elapsed]
yandex_compute_instance.node05: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [40s elapsed]
yandex_compute_instance.node04: Still creating... [40s elapsed]
yandex_compute_instance.node02: Still creating... [40s elapsed]
yandex_compute_instance.node03: Still creating... [40s elapsed]
yandex_compute_instance.node05: Still creating... [40s elapsed]
yandex_compute_instance.node05: Creation complete after 43s [id=fhmjne2t0jcqb92pktbp]
yandex_compute_instance.node01: Creation complete after 44s [id=fhm0rjjk26hvgiuosqt3]
yandex_compute_instance.node04: Creation complete after 45s [id=fhmn17a0doot7ptjmvt1]
yandex_compute_instance.node02: Creation complete after 46s [id=fhm0pmt4mtqochahp26e]
yandex_compute_instance.node03: Creation complete after 46s [id=fhm5a7em5soe1enkvm5u]
local_file.inventory: Creating...
local_file.inventory: Creation complete after 0s [id=7082f357ecd60870dfd4e1b01e7f109e030ceb29]
null_resource.wait: Creating...
null_resource.wait: Provisioning with 'local-exec'...
null_resource.wait (local-exec): Executing: ["/bin/sh" "-c" "sleep 100"]
null_resource.wait: Still creating... [10s elapsed]
null_resource.wait: Still creating... [20s elapsed]
null_resource.wait: Still creating... [30s elapsed]
null_resource.wait: Still creating... [40s elapsed]
null_resource.wait: Still creating... [50s elapsed]
null_resource.wait: Still creating... [1m0s elapsed]
null_resource.wait: Still creating... [1m10s elapsed]
null_resource.wait: Still creating... [1m20s elapsed]
null_resource.wait: Still creating... [1m30s elapsed]
null_resource.wait: Creation complete after 1m40s [id=394699306227522902]
null_resource.cluster: Creating...
null_resource.cluster: Provisioning with 'local-exec'...
null_resource.cluster (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-cluster.yml"]

null_resource.cluster (local-exec): PLAY [Install of Requrements Tools] ********************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [install-tools : Installing tools] ****************************************
null_resource.cluster: Still creating... [10s elapsed]
null_resource.cluster: Still creating... [20s elapsed]
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [30s elapsed]
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [40s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [configure-hosts-file : Configure Hosts File] *****************************
null_resource.cluster: Still creating... [50s elapsed]
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Install Docker Engine] ***************************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster: Still creating... [1m0s elapsed]
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Add docker repository] *****************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Installing docker package] *************************
null_resource.cluster: Still creating... [1m10s elapsed]
null_resource.cluster: Still creating... [1m20s elapsed]
null_resource.cluster: Still creating... [1m30s elapsed]
null_resource.cluster: Still creating... [1m40s elapsed]
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [1m50s elapsed]
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [2m0s elapsed]
null_resource.cluster: Still creating... [2m10s elapsed]
null_resource.cluster: Still creating... [2m20s elapsed]
null_resource.cluster: Still creating... [2m30s elapsed]
null_resource.cluster: Still creating... [2m40s elapsed]
null_resource.cluster: Still creating... [2m50s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Enable docker daemon] ******************************
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [3m0s elapsed]
null_resource.cluster: Still creating... [3m10s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Initialize Docker Swarm Cluster] *****************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Initialize Docker Swarm] *****************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Get the Manager join-token] **************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Get the worker join-token] ***************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Add Managers Swarm Cluster] **********************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster: Still creating... [3m20s elapsed]
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-add-manager : Add Managers to the Swarm] ********************
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Add Workers to the Swarm Cluster] ****************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-add-worker : Add Workers to the Swarm] **********************
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY RECAP *********************************************************************
null_resource.cluster (local-exec): node01.netology.yc         : ok=11   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node02.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node03.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node04.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node05.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node06.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

null_resource.cluster: Creation complete after 3m27s [id=8434585004882673678]
null_resource.sync: Creating...
null_resource.sync: Provisioning with 'local-exec'...
null_resource.sync (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-sync.yml"]

null_resource.sync (local-exec): PLAY [nodes] *******************************************************************

null_resource.sync (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.sync (local-exec): ok: [node01.netology.yc]
null_resource.sync (local-exec): ok: [node05.netology.yc]
null_resource.sync (local-exec): ok: [node02.netology.yc]
null_resource.sync (local-exec): ok: [node04.netology.yc]
null_resource.sync (local-exec): ok: [node06.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): ok: [node03.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): TASK [Synchronization] *********************************************************
null_resource.sync: Still creating... [10s elapsed]
null_resource.sync: Still creating... [20s elapsed]
null_resource.sync: Still creating... [30s elapsed]
null_resource.sync: Still creating... [40s elapsed]
null_resource.sync: Still creating... [50s elapsed]
null_resource.sync (local-exec): changed: [node01.netology.yc]
null_resource.sync (local-exec): changed: [node05.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node02.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node04.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node06.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync: Still creating... [1m0s elapsed]
null_resource.sync: Still creating... [1m10s elapsed]
null_resource.sync: Still creating... [1m20s elapsed]
null_resource.sync: Still creating... [1m30s elapsed]
null_resource.sync (local-exec): changed: [node03.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): PLAY RECAP *********************************************************************
null_resource.sync (local-exec): node01.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node02.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node03.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node04.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node05.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node06.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

null_resource.sync: Creation complete after 1m35s [id=6381639646372307869]
null_resource.monitoring: Creating...
null_resource.monitoring: Provisioning with 'local-exec'...
null_resource.monitoring (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-stack.yml --limit=managers"]

null_resource.monitoring (local-exec): PLAY [nodes] *******************************************************************

null_resource.monitoring (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.monitoring (local-exec): ok: [node01.netology.yc]
null_resource.monitoring (local-exec): ok: [node02.netology.yc]
null_resource.monitoring (local-exec): ok: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): TASK [Check Current Leader] ****************************************************
null_resource.monitoring (local-exec): ok: [node02.netology.yc]
null_resource.monitoring (local-exec): ok: [node01.netology.yc]
null_resource.monitoring (local-exec): ok: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): TASK [Run deploy, if node is leader] *******************************************
null_resource.monitoring (local-exec): skipping: [node02.netology.yc]
null_resource.monitoring (local-exec): skipping: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring: Still creating... [10s elapsed]
null_resource.monitoring: Still creating... [20s elapsed]
null_resource.monitoring: Still creating... [30s elapsed]
null_resource.monitoring (local-exec): fatal: [node01.netology.yc]: FAILED! => {"changed": true, "cmd": "docker stack deploy --compose-file /opt/monitoring/docker-compose.yml swarm_monitoring", "delta": "0:00:25.689835", "end": "2021-12-11 18:58:07.744135", "msg": "non-zero return code", "rc": 1, "start": "2021-12-11 18:57:42.054300", "stderr": "failed to create service swarm_monitoring_unsee: Error response from daemon: rpc error: code = Unknown desc = raft: failed to process the request: node lost leader status", "stderr_lines": ["failed to create service swarm_monitoring_unsee: Error response from daemon: rpc error: code = Unknown desc = raft: failed to process the request: node lost leader status"], "stdout": "Creating network swarm_monitoring_net\nCreating config swarm_monitoring_task_rules\nCreating config swarm_monitoring_caddy_config\nCreating config swarm_monitoring_dockerd_config\nCreating config swarm_monitoring_node_rules\nCreating service swarm_monitoring_dockerd-exporter\nCreating service swarm_monitoring_cadvisor\nCreating service swarm_monitoring_grafana\nCreating service swarm_monitoring_alertmanager\nCreating service swarm_monitoring_unsee", "stdout_lines": ["Creating network swarm_monitoring_net", "Creating config swarm_monitoring_task_rules", "Creating config swarm_monitoring_caddy_config", "Creating config swarm_monitoring_dockerd_config", "Creating config swarm_monitoring_node_rules", "Creating service swarm_monitoring_dockerd-exporter", "Creating service swarm_monitoring_cadvisor", "Creating service swarm_monitoring_grafana", "Creating service swarm_monitoring_alertmanager", "Creating service swarm_monitoring_unsee"]}
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): PLAY RECAP *********************************************************************
null_resource.monitoring (local-exec): node01.netology.yc         : ok=2    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0
null_resource.monitoring (local-exec): node02.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
null_resource.monitoring (local-exec): node03.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

╷
│ Error: local-exec provisioner error
│ 
│   with null_resource.monitoring,
│   on ansible.tf line 32, in resource "null_resource" "monitoring":
│   32:   provisioner "local-exec" {
│ 
│ Error running command 'ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-stack.yml --limit=managers': exit status 2. Output: 
│ PLAY [nodes] *******************************************************************
│ 
│ TASK [Gathering Facts] *********************************************************
│ ok: [node01.netology.yc]
│ ok: [node02.netology.yc]
│ ok: [node03.netology.yc]
│ 
│ TASK [Check Current Leader] ****************************************************
│ ok: [node02.netology.yc]
│ ok: [node01.netology.yc]
│ ok: [node03.netology.yc]
│ 
│ TASK [Run deploy, if node is leader] *******************************************
│ skipping: [node02.netology.yc]
│ skipping: [node03.netology.yc]
│ fatal: [node01.netology.yc]: FAILED! => {"changed": true, "cmd": "docker stack deploy --compose-file /opt/monitoring/docker-compose.yml swarm_monitoring", "delta": "0:00:25.689835",
│ "end": "2021-12-11 18:58:07.744135", "msg": "non-zero return code", "rc": 1, "start": "2021-12-11 18:57:42.054300", "stderr": "failed to create service swarm_monitoring_unsee: Error response from daemon:
│ rpc error: code = Unknown desc = raft: failed to process the request: node lost leader status", "stderr_lines": ["failed to create service swarm_monitoring_unsee: Error response from daemon: rpc error:
│ code = Unknown desc = raft: failed to process the request: node lost leader status"], "stdout": "Creating network swarm_monitoring_net\nCreating config swarm_monitoring_task_rules\nCreating config
│ swarm_monitoring_caddy_config\nCreating config swarm_monitoring_dockerd_config\nCreating config swarm_monitoring_node_rules\nCreating service swarm_monitoring_dockerd-exporter\nCreating service
│ swarm_monitoring_cadvisor\nCreating service swarm_monitoring_grafana\nCreating service swarm_monitoring_alertmanager\nCreating service swarm_monitoring_unsee", "stdout_lines": ["Creating network
│ swarm_monitoring_net", "Creating config swarm_monitoring_task_rules", "Creating config swarm_monitoring_caddy_config", "Creating config swarm_monitoring_dockerd_config", "Creating config
│ swarm_monitoring_node_rules", "Creating service swarm_monitoring_dockerd-exporter", "Creating service swarm_monitoring_cadvisor", "Creating service swarm_monitoring_grafana", "Creating service
│ swarm_monitoring_alertmanager", "Creating service swarm_monitoring_unsee"]}
│ 
│ PLAY RECAP *********************************************************************
│ node01.netology.yc         : ok=2    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
│ node02.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
│ node03.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
│ 
│ 

```
##### Удаление ВМ после неудачного их создания
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform destroy -auto-approve
yandex_vpc_network.default: Refreshing state... [id=enphkubv2mkhbjhs9hs1]
yandex_vpc_subnet.default: Refreshing state... [id=e9b814rva083lct8fq02]
yandex_compute_instance.node06: Refreshing state... [id=fhm66homrnuh7j49td8u]
yandex_compute_instance.node05: Refreshing state... [id=fhmjne2t0jcqb92pktbp]
yandex_compute_instance.node02: Refreshing state... [id=fhm0pmt4mtqochahp26e]
yandex_compute_instance.node01: Refreshing state... [id=fhm0rjjk26hvgiuosqt3]
yandex_compute_instance.node03: Refreshing state... [id=fhm5a7em5soe1enkvm5u]
yandex_compute_instance.node04: Refreshing state... [id=fhmn17a0doot7ptjmvt1]
local_file.inventory: Refreshing state... [id=7082f357ecd60870dfd4e1b01e7f109e030ceb29]
null_resource.wait: Refreshing state... [id=394699306227522902]
null_resource.cluster: Refreshing state... [id=8434585004882673678]
null_resource.sync: Refreshing state... [id=6381639646372307869]
null_resource.monitoring: Refreshing state... [id=3410425302826177165]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # local_file.inventory will be destroyed
  - resource "local_file" "inventory" {
      - content              = <<-EOT
            # Ansible inventory containing variable values from Terraform.
            # Generated by Terraform.
            
            [nodes:children]
            managers
            workers
            
            [managers:children]
            active
            standby
            
            [active]
            node01.netology.yc ansible_host=51.250.3.239
            
            [standby]
            node02.netology.yc ansible_host=62.84.115.90
            node03.netology.yc ansible_host=51.250.12.188
            
            [workers]
            node04.netology.yc ansible_host=62.84.115.205
            node05.netology.yc ansible_host=62.84.115.160
            node06.netology.yc ansible_host=62.84.113.68
        EOT -> null
      - directory_permission = "0777" -> null
      - file_permission      = "0777" -> null
      - filename             = "../ansible/inventory" -> null
      - id                   = "7082f357ecd60870dfd4e1b01e7f109e030ceb29" -> null
    }

  # null_resource.cluster will be destroyed
  - resource "null_resource" "cluster" {
      - id = "8434585004882673678" -> null
    }

  # null_resource.monitoring will be destroyed
  - resource "null_resource" "monitoring" {
      - id = "3410425302826177165" -> null
    }

  # null_resource.sync will be destroyed
  - resource "null_resource" "sync" {
      - id = "6381639646372307869" -> null
    }

  # null_resource.wait will be destroyed
  - resource "null_resource" "wait" {
      - id = "394699306227522902" -> null
    }

  # yandex_compute_instance.node01 will be destroyed
  - resource "yandex_compute_instance" "node01" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node01.netology.yc" -> null
      - hostname                  = "node01" -> null
      - id                        = "fhm0rjjk26hvgiuosqt3" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node01" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmg5b7p07743cktkdgf" -> null
          - disk_id     = "fhmg5b7p07743cktkdgf" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node01" -> null
              - size     = 10 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.11" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:dc:e7:41:1a" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.3.239" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node02 will be destroyed
  - resource "yandex_compute_instance" "node02" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node02.netology.yc" -> null
      - hostname                  = "node02" -> null
      - id                        = "fhm0pmt4mtqochahp26e" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node02" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhm74v340c9ipcfm45f0" -> null
          - disk_id     = "fhm74v340c9ipcfm45f0" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node02" -> null
              - size     = 10 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.12" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:cd:ba:4b:77" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.115.90" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node03 will be destroyed
  - resource "yandex_compute_instance" "node03" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node03.netology.yc" -> null
      - hostname                  = "node03" -> null
      - id                        = "fhm5a7em5soe1enkvm5u" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node03" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmo5mgmdqafh77ah3ek" -> null
          - disk_id     = "fhmo5mgmdqafh77ah3ek" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node03" -> null
              - size     = 10 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.13" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:55:1d:d6:2f" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.12.188" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node04 will be destroyed
  - resource "yandex_compute_instance" "node04" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node04.netology.yc" -> null
      - hostname                  = "node04" -> null
      - id                        = "fhmn17a0doot7ptjmvt1" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node04" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhm5st4atil4e4u9q7dr" -> null
          - disk_id     = "fhm5st4atil4e4u9q7dr" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node04" -> null
              - size     = 40 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.14" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:17:09:d4:06" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.115.205" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node05 will be destroyed
  - resource "yandex_compute_instance" "node05" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node05.netology.yc" -> null
      - hostname                  = "node05" -> null
      - id                        = "fhmjne2t0jcqb92pktbp" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node05" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmrdue1tm2cs9u01epu" -> null
          - disk_id     = "fhmrdue1tm2cs9u01epu" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node05" -> null
              - size     = 40 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.15" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:13:bb:85:d0" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.115.160" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node06 will be destroyed
  - resource "yandex_compute_instance" "node06" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T18:50:08Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node06.netology.yc" -> null
      - hostname                  = "node06" -> null
      - id                        = "fhm66homrnuh7j49td8u" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node06" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmcuguj169ujq1r3ebe" -> null
          - disk_id     = "fhmcuguj169ujq1r3ebe" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node06" -> null
              - size     = 40 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.16" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:63:47:16:dd" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.113.68" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9b814rva083lct8fq02" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_vpc_network.default will be destroyed
  - resource "yandex_vpc_network" "default" {
      - created_at = "2021-12-11T18:50:06Z" -> null
      - folder_id  = "b1gd3hm4niaifoa8dahm" -> null
      - id         = "enphkubv2mkhbjhs9hs1" -> null
      - labels     = {} -> null
      - name       = "net" -> null
      - subnet_ids = [
          - "e9b814rva083lct8fq02",
        ] -> null
    }

  # yandex_vpc_subnet.default will be destroyed
  - resource "yandex_vpc_subnet" "default" {
      - created_at     = "2021-12-11T18:50:07Z" -> null
      - folder_id      = "b1gd3hm4niaifoa8dahm" -> null
      - id             = "e9b814rva083lct8fq02" -> null
      - labels         = {} -> null
      - name           = "subnet" -> null
      - network_id     = "enphkubv2mkhbjhs9hs1" -> null
      - v4_cidr_blocks = [
          - "192.168.101.0/24",
        ] -> null
      - v6_cidr_blocks = [] -> null
      - zone           = "ru-central1-a" -> null
    }

Plan: 0 to add, 0 to change, 13 to destroy.

Changes to Outputs:
  - external_ip_address_node01 = "51.250.3.239" -> null
  - external_ip_address_node02 = "62.84.115.90" -> null
  - external_ip_address_node03 = "51.250.12.188" -> null
  - external_ip_address_node04 = "62.84.115.205" -> null
  - external_ip_address_node05 = "62.84.115.160" -> null
  - external_ip_address_node06 = "62.84.113.68" -> null
  - internal_ip_address_node01 = "192.168.101.11" -> null
  - internal_ip_address_node02 = "192.168.101.12" -> null
  - internal_ip_address_node03 = "192.168.101.13" -> null
  - internal_ip_address_node04 = "192.168.101.14" -> null
  - internal_ip_address_node05 = "192.168.101.15" -> null
  - internal_ip_address_node06 = "192.168.101.16" -> null
null_resource.monitoring: Destroying... [id=3410425302826177165]
null_resource.monitoring: Destruction complete after 0s
null_resource.sync: Destroying... [id=6381639646372307869]
null_resource.sync: Destruction complete after 0s
null_resource.cluster: Destroying... [id=8434585004882673678]
null_resource.cluster: Destruction complete after 0s
null_resource.wait: Destroying... [id=394699306227522902]
null_resource.wait: Destruction complete after 0s
local_file.inventory: Destroying... [id=7082f357ecd60870dfd4e1b01e7f109e030ceb29]
local_file.inventory: Destruction complete after 0s
yandex_compute_instance.node06: Destroying... [id=fhm66homrnuh7j49td8u]
yandex_compute_instance.node04: Destroying... [id=fhmn17a0doot7ptjmvt1]
yandex_compute_instance.node03: Destroying... [id=fhm5a7em5soe1enkvm5u]
yandex_compute_instance.node05: Destroying... [id=fhmjne2t0jcqb92pktbp]
yandex_compute_instance.node01: Destroying... [id=fhm0rjjk26hvgiuosqt3]
yandex_compute_instance.node02: Destroying... [id=fhm0pmt4mtqochahp26e]
yandex_compute_instance.node06: Still destroying... [id=fhm66homrnuh7j49td8u, 10s elapsed]
yandex_compute_instance.node04: Still destroying... [id=fhmn17a0doot7ptjmvt1, 10s elapsed]
yandex_compute_instance.node03: Still destroying... [id=fhm5a7em5soe1enkvm5u, 10s elapsed]
yandex_compute_instance.node05: Still destroying... [id=fhmjne2t0jcqb92pktbp, 10s elapsed]
yandex_compute_instance.node02: Still destroying... [id=fhm0pmt4mtqochahp26e, 10s elapsed]
yandex_compute_instance.node01: Still destroying... [id=fhm0rjjk26hvgiuosqt3, 10s elapsed]
yandex_compute_instance.node01: Destruction complete after 12s
yandex_compute_instance.node06: Destruction complete after 12s
yandex_compute_instance.node03: Destruction complete after 13s
yandex_compute_instance.node04: Destruction complete after 14s
yandex_compute_instance.node02: Destruction complete after 14s
yandex_compute_instance.node05: Destruction complete after 16s
yandex_vpc_subnet.default: Destroying... [id=e9b814rva083lct8fq02]
yandex_vpc_subnet.default: Destruction complete after 3s
yandex_vpc_network.default: Destroying... [id=enphkubv2mkhbjhs9hs1]
yandex_vpc_network.default: Destruction complete after 0s

Destroy complete! Resources: 13 destroyed.
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
```
##### Успешное создание ВМ и выполнение команды ` terraform apply -auto-approve `
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of yandex-cloud/yandex from the dependency lock file
- Reusing previous version of hashicorp/null from the dependency lock file
- Reusing previous version of hashicorp/local from the dependency lock file
- Using previously-installed yandex-cloud/yandex v0.68.0
- Using previously-installed hashicorp/null v3.1.0
- Using previously-installed hashicorp/local v2.1.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform validate
Success! The configuration is valid.

root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.inventory will be created
  + resource "local_file" "inventory" {
      + content              = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "../ansible/inventory"
      + id                   = (known after apply)
    }

  # null_resource.cluster will be created
  + resource "null_resource" "cluster" {
      + id = (known after apply)
    }

  # null_resource.monitoring will be created
  + resource "null_resource" "monitoring" {
      + id = (known after apply)
    }

  # null_resource.sync will be created
  + resource "null_resource" "sync" {
      + id = (known after apply)
    }

  # null_resource.wait will be created
  + resource "null_resource" "wait" {
      + id = (known after apply)
    }

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

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node02"
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
              + name        = "root-node02"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.12"
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

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node03"
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
              + name        = "root-node03"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.13"
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

  # yandex_compute_instance.node04 will be created
  + resource "yandex_compute_instance" "node04" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node04.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node04"
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
              + name        = "root-node04"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.14"
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

  # yandex_compute_instance.node05 will be created
  + resource "yandex_compute_instance" "node05" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node05.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node05"
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
              + name        = "root-node05"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.15"
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

  # yandex_compute_instance.node06 will be created
  + resource "yandex_compute_instance" "node06" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node06.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node06"
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
              + name        = "root-node06"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.16"
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
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 13 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01 = (known after apply)
  + external_ip_address_node02 = (known after apply)
  + external_ip_address_node03 = (known after apply)
  + external_ip_address_node04 = (known after apply)
  + external_ip_address_node05 = (known after apply)
  + external_ip_address_node06 = (known after apply)
  + internal_ip_address_node01 = "192.168.101.11"
  + internal_ip_address_node02 = "192.168.101.12"
  + internal_ip_address_node03 = "192.168.101.13"
  + internal_ip_address_node04 = "192.168.101.14"
  + internal_ip_address_node05 = "192.168.101.15"
  + internal_ip_address_node06 = "192.168.101.16"
yandex_vpc_network.default: Creating...
yandex_vpc_network.default: Creation complete after 1s [id=enpc312d4skup1ih9f56]
yandex_vpc_subnet.default: Creating...
yandex_vpc_subnet.default: Creation complete after 0s [id=e9bht3uldnh4tt3u6eps]
yandex_compute_instance.node03: Creating...
yandex_compute_instance.node02: Creating...
yandex_compute_instance.node06: Creating...
yandex_compute_instance.node04: Creating...
yandex_compute_instance.node05: Creating...
yandex_compute_instance.node01: Creating...
yandex_compute_instance.node06: Still creating... [10s elapsed]
yandex_compute_instance.node02: Still creating... [10s elapsed]
yandex_compute_instance.node03: Still creating... [10s elapsed]
yandex_compute_instance.node04: Still creating... [10s elapsed]
yandex_compute_instance.node05: Still creating... [10s elapsed]
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node02: Still creating... [20s elapsed]
yandex_compute_instance.node06: Still creating... [20s elapsed]
yandex_compute_instance.node03: Still creating... [20s elapsed]
yandex_compute_instance.node05: Still creating... [20s elapsed]
yandex_compute_instance.node04: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node06: Still creating... [30s elapsed]
yandex_compute_instance.node03: Still creating... [30s elapsed]
yandex_compute_instance.node02: Still creating... [30s elapsed]
yandex_compute_instance.node04: Still creating... [30s elapsed]
yandex_compute_instance.node05: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node02: Still creating... [40s elapsed]
yandex_compute_instance.node06: Still creating... [40s elapsed]
yandex_compute_instance.node03: Still creating... [40s elapsed]
yandex_compute_instance.node05: Still creating... [40s elapsed]
yandex_compute_instance.node04: Still creating... [40s elapsed]
yandex_compute_instance.node01: Still creating... [40s elapsed]
yandex_compute_instance.node06: Creation complete after 42s [id=fhmq93ema4bsnrnijjnn]
yandex_compute_instance.node03: Creation complete after 43s [id=fhm6ecqjl7nqqi1u87gf]
yandex_compute_instance.node02: Creation complete after 44s [id=fhm2t4posqgnli5k2v65]
yandex_compute_instance.node01: Creation complete after 45s [id=fhm89vveosnbvofjoh6k]
yandex_compute_instance.node05: Creation complete after 46s [id=fhm982u53nfl22v9f3es]
yandex_compute_instance.node04: Still creating... [50s elapsed]
yandex_compute_instance.node04: Creation complete after 54s [id=fhmagbn8dijah7g55499]
local_file.inventory: Creating...
local_file.inventory: Creation complete after 0s [id=822c233c44b0cbd0bb4c31500ecbca5e7847e6c5]
null_resource.wait: Creating...
null_resource.wait: Provisioning with 'local-exec'...
null_resource.wait (local-exec): Executing: ["/bin/sh" "-c" "sleep 100"]
null_resource.wait: Still creating... [10s elapsed]
null_resource.wait: Still creating... [20s elapsed]
null_resource.wait: Still creating... [30s elapsed]
null_resource.wait: Still creating... [40s elapsed]
null_resource.wait: Still creating... [50s elapsed]
null_resource.wait: Still creating... [1m0s elapsed]
null_resource.wait: Still creating... [1m10s elapsed]
null_resource.wait: Still creating... [1m20s elapsed]
null_resource.wait: Still creating... [1m30s elapsed]
null_resource.wait: Creation complete after 1m40s [id=6789423876241631478]
null_resource.cluster: Creating...
null_resource.cluster: Provisioning with 'local-exec'...
null_resource.cluster (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-cluster.yml"]

null_resource.cluster (local-exec): PLAY [Install of Requrements Tools] ********************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [install-tools : Installing tools] ****************************************
null_resource.cluster: Still creating... [10s elapsed]
null_resource.cluster: Still creating... [20s elapsed]
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [30s elapsed]
null_resource.cluster: Still creating... [40s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=['ntp', 'python', 'tcpdump', 'wget', 'openssl', 'curl', 'git'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [configure-hosts-file : Configure Hosts File] *****************************
null_resource.cluster: Still creating... [50s elapsed]
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node04.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node05.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node06.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node01.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node02.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=node03.netology.yc)
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Install Docker Engine] ***************************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [1m0s elapsed]
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Add docker repository] *****************************
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Installing docker package] *************************
null_resource.cluster: Still creating... [1m10s elapsed]
null_resource.cluster: Still creating... [1m20s elapsed]
null_resource.cluster: Still creating... [1m30s elapsed]
null_resource.cluster (local-exec): changed: [node04.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [1m40s elapsed]
null_resource.cluster (local-exec): changed: [node05.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node02.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node01.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [1m50s elapsed]
null_resource.cluster: Still creating... [2m0s elapsed]
null_resource.cluster: Still creating... [2m10s elapsed]
null_resource.cluster: Still creating... [2m20s elapsed]
null_resource.cluster: Still creating... [2m30s elapsed]
null_resource.cluster: Still creating... [2m40s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc] => (item=['docker-ce', 'docker-ce-cli', 'containerd.io'])
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-installation : Enable docker daemon] ******************************
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster: Still creating... [2m50s elapsed]
null_resource.cluster: Still creating... [3m0s elapsed]
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Initialize Docker Swarm Cluster] *****************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Initialize Docker Swarm] *****************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Get the Manager join-token] **************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-init : Get the worker join-token] ***************************
null_resource.cluster (local-exec): changed: [node01.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Add Managers Swarm Cluster] **********************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster: Still creating... [3m10s elapsed]
null_resource.cluster (local-exec): ok: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): ok: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-add-manager : Add Managers to the Swarm] ********************
null_resource.cluster (local-exec): changed: [node02.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node03.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY [Add Workers to the Swarm Cluster] ****************************************

null_resource.cluster (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.cluster (local-exec): ok: [node04.netology.yc]
null_resource.cluster (local-exec): ok: [node05.netology.yc]
null_resource.cluster (local-exec): ok: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): TASK [docker-swarm-add-worker : Add Workers to the Swarm] **********************
null_resource.cluster (local-exec): changed: [node04.netology.yc]
null_resource.cluster (local-exec): changed: [node05.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): changed: [node06.netology.yc]
null_resource.cluster (local-exec): 
null_resource.cluster (local-exec): PLAY RECAP *********************************************************************
null_resource.cluster (local-exec): node01.netology.yc         : ok=11   changed=8    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node02.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node03.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node04.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node05.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.cluster (local-exec): node06.netology.yc         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

null_resource.cluster: Creation complete after 3m17s [id=7624586587786292199]
null_resource.sync: Creating...
null_resource.sync: Provisioning with 'local-exec'...
null_resource.sync (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-sync.yml"]

null_resource.sync (local-exec): PLAY [nodes] *******************************************************************

null_resource.sync (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.sync (local-exec): ok: [node02.netology.yc]
null_resource.sync (local-exec): ok: [node04.netology.yc]
null_resource.sync (local-exec): ok: [node01.netology.yc]
null_resource.sync (local-exec): ok: [node05.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): ok: [node06.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): ok: [node03.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): TASK [Synchronization] *********************************************************
null_resource.sync: Still creating... [10s elapsed]
null_resource.sync: Still creating... [20s elapsed]
null_resource.sync: Still creating... [30s elapsed]
null_resource.sync: Still creating... [40s elapsed]
null_resource.sync (local-exec): changed: [node04.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node02.netology.yc]
null_resource.sync (local-exec): changed: [node01.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node05.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): changed: [node06.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync: Still creating... [50s elapsed]
null_resource.sync: Still creating... [1m0s elapsed]
null_resource.sync: Still creating... [1m10s elapsed]
null_resource.sync: Still creating... [1m21s elapsed]
null_resource.sync (local-exec): changed: [node03.netology.yc]
null_resource.sync (local-exec): 
null_resource.sync (local-exec): PLAY RECAP *********************************************************************
null_resource.sync (local-exec): node01.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node02.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node03.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node04.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node05.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.sync (local-exec): node06.netology.yc         : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

null_resource.sync: Creation complete after 1m26s [id=1493800218186160928]
null_resource.monitoring: Creating...
null_resource.monitoring: Provisioning with 'local-exec'...
null_resource.monitoring (local-exec): Executing: ["/bin/sh" "-c" "ANSIBLE_FORCE_COLOR=1 ansible-playbook -i ../ansible/inventory ../ansible/swarm-deploy-stack.yml --limit=managers"]

null_resource.monitoring (local-exec): PLAY [nodes] *******************************************************************

null_resource.monitoring (local-exec): TASK [Gathering Facts] *********************************************************
null_resource.monitoring (local-exec): ok: [node02.netology.yc]
null_resource.monitoring (local-exec): ok: [node01.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): ok: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): TASK [Check Current Leader] ****************************************************
null_resource.monitoring (local-exec): ok: [node02.netology.yc]
null_resource.monitoring (local-exec): ok: [node01.netology.yc]
null_resource.monitoring (local-exec): ok: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): TASK [Run deploy, if node is leader] *******************************************
null_resource.monitoring (local-exec): skipping: [node02.netology.yc]
null_resource.monitoring (local-exec): skipping: [node03.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring: Still creating... [10s elapsed]
null_resource.monitoring: Still creating... [20s elapsed]
null_resource.monitoring: Still creating... [30s elapsed]
null_resource.monitoring (local-exec): changed: [node01.netology.yc]
null_resource.monitoring (local-exec): 
null_resource.monitoring (local-exec): PLAY RECAP *********************************************************************
null_resource.monitoring (local-exec): node01.netology.yc         : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
null_resource.monitoring (local-exec): node02.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
null_resource.monitoring (local-exec): node03.netology.yc         : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

null_resource.monitoring: Creation complete after 37s [id=3787288271240279675]

Apply complete! Resources: 13 added, 0 changed, 0 destroyed.

Outputs:

external_ip_address_node01 = "51.250.14.241"
external_ip_address_node02 = "51.250.1.227"
external_ip_address_node03 = "51.250.4.178"
external_ip_address_node04 = "51.250.6.118"
external_ip_address_node05 = "51.250.1.53"
external_ip_address_node06 = "51.250.1.149"
internal_ip_address_node01 = "192.168.101.11"
internal_ip_address_node02 = "192.168.101.12"
internal_ip_address_node03 = "192.168.101.13"
internal_ip_address_node04 = "192.168.101.14"
internal_ip_address_node05 = "192.168.101.15"
internal_ip_address_node06 = "192.168.101.16"
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# 

```
#### 5. Создаём Docker Swarm кластер из виртуальных машин, созданных на предыдущем шаге.

#### 6. Запускаем деплой стека приложений.
#### 7. Проводим стресс тест Docker Swarm кластера.
- Заходим по ssh на одну из нод.
```bash
root@PC-Ubuntu:~# ssh centos@51.250.1.227
[centos@node02 ~]$ 
[centos@node02 ~]$ 
[centos@node02 ~]$ sudo -i
[root@node02 ~]# 
[root@node02 ~]# 
```
```bash
[root@node02 ~]# docker node ls
ID                            HOSTNAME             STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
qjmezayny3c6c5kaf8b6i8v5e     node01.netology.yc   Ready     Active         Leader           20.10.11
bqre35lordbvn4rtwtlign6no *   node02.netology.yc   Ready     Active         Reachable        20.10.11
zfbbdwqxrdzorocfb9kp92hfa     node03.netology.yc   Ready     Active         Reachable        20.10.11
nba4ua0v5u7k7xh2upall2w8w     node04.netology.yc   Ready     Active                          20.10.11
w8a5dn2em5f85lsgviinp9v3z     node05.netology.yc   Ready     Active                          20.10.11
j69md7ol8z6bp5w3gqp61jfsw     node06.netology.yc   Ready     Active                          20.10.11

```
Мы сейчас находимся на ноде bqre35lordbvn4rtwtlign6no, где знак *
Переходим на ноду-лидер и перезагружаем ее.
При этом docker-swarm определяет лидером другую ноду
```bash
root@node02 ~]# docker node ls
ID                            HOSTNAME             STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
qjmezayny3c6c5kaf8b6i8v5e     node01.netology.yc   Unknown   Active         Unreachable      20.10.11
bqre35lordbvn4rtwtlign6no *   node02.netology.yc   Unknown   Active         Leader           20.10.11
zfbbdwqxrdzorocfb9kp92hfa     node03.netology.yc   Ready     Active         Reachable        20.10.11
nba4ua0v5u7k7xh2upall2w8w     node04.netology.yc   Unknown   Active                          20.10.11
w8a5dn2em5f85lsgviinp9v3z     node05.netology.yc   Unknown   Active                          20.10.11
j69md7ol8z6bp5w3gqp61jfsw     node06.netology.yc   Ready     Active                          20.10.11

```
#### Смотрим состояние стека микросервисов
##### Узнаем имя стека
```bash
[root@node02 ~]# docker stack ls
NAME               SERVICES   ORCHESTRATOR
swarm_monitoring   8          Swarm

```
##### Состояние стека микросервисов
```bash
[root@node02 ~]# cd /opt/monitoring/
[root@node02 monitoring]# 
[root@node02 monitoring]# docker stack ps swarm_monitoring | less
[root@node02 monitoring]# 
[root@node02 monitoring]# docker stack ps swarm_monitoring
ID             NAME                                                              IMAGE                                          NODE                 DESIRED STATE   CURRENT STATE          ERROR     PORTS
a641aosfxwfy   swarm_monitoring_alertmanager.1                                   stefanprodan/swarmprom-alertmanager:v0.14.0    node02.netology.yc   Running         Running 2 hours ago              
np4iqkjzvq09   swarm_monitoring_caddy.1                                          stefanprodan/caddy:latest                      node02.netology.yc   Running         Running 2 hours ago              
xxbrpyco6z2u    \_ swarm_monitoring_caddy.1                                      stefanprodan/caddy:latest                      node02.netology.yc   Shutdown        Complete 3 hours ago             
sc83buaycxyj   swarm_monitoring_cadvisor.bqre35lordbvn4rtwtlign6no               google/cadvisor:latest                         node02.netology.yc   Running         Running 2 hours ago              
15apxmrlddyc   swarm_monitoring_cadvisor.j69md7ol8z6bp5w3gqp61jfsw               google/cadvisor:latest                         node06.netology.yc   Running         Running 2 hours ago              
90cxdb99ync6   swarm_monitoring_cadvisor.nba4ua0v5u7k7xh2upall2w8w               google/cadvisor:latest                         node04.netology.yc   Running         Running 2 hours ago              
xbshc3c45260   swarm_monitoring_cadvisor.qjmezayny3c6c5kaf8b6i8v5e               google/cadvisor:latest                         node01.netology.yc   Running         Running 2 hours ago              
zm0b51r1q7ta    \_ swarm_monitoring_cadvisor.qjmezayny3c6c5kaf8b6i8v5e           google/cadvisor:latest                         node01.netology.yc   Shutdown        Shutdown 2 hours ago             
l7p2kejd6n8o   swarm_monitoring_cadvisor.w8a5dn2em5f85lsgviinp9v3z               google/cadvisor:latest                         node05.netology.yc   Running         Running 2 hours ago              
e5ro813zalgr   swarm_monitoring_cadvisor.zfbbdwqxrdzorocfb9kp92hfa               google/cadvisor:latest                         node03.netology.yc   Running         Running 2 hours ago              
nt9ok9j30s2i   swarm_monitoring_dockerd-exporter.bqre35lordbvn4rtwtlign6no       stefanprodan/caddy:latest                      node02.netology.yc   Running         Running 2 hours ago              
yoemj2bapygy   swarm_monitoring_dockerd-exporter.j69md7ol8z6bp5w3gqp61jfsw       stefanprodan/caddy:latest                      node06.netology.yc   Running         Running 2 hours ago              
95jpbhdv72mz   swarm_monitoring_dockerd-exporter.nba4ua0v5u7k7xh2upall2w8w       stefanprodan/caddy:latest                      node04.netology.yc   Running         Running 2 hours ago              
hujnpr44vm8w   swarm_monitoring_dockerd-exporter.qjmezayny3c6c5kaf8b6i8v5e       stefanprodan/caddy:latest                      node01.netology.yc   Running         Running 2 hours ago              
231v7jpjs6pc    \_ swarm_monitoring_dockerd-exporter.qjmezayny3c6c5kaf8b6i8v5e   stefanprodan/caddy:latest                      node01.netology.yc   Shutdown        Shutdown 2 hours ago             
wsp3hho32epg   swarm_monitoring_dockerd-exporter.w8a5dn2em5f85lsgviinp9v3z       stefanprodan/caddy:latest                      node05.netology.yc   Running         Running 2 hours ago              
xv5uarkjk4vl   swarm_monitoring_dockerd-exporter.zfbbdwqxrdzorocfb9kp92hfa       stefanprodan/caddy:latest                      node03.netology.yc   Running         Running 2 hours ago              
welag2jjx2qy   swarm_monitoring_grafana.1                                        stefanprodan/swarmprom-grafana:5.3.4           node03.netology.yc   Running         Running 2 hours ago              
woefql4e1x8a   swarm_monitoring_node-exporter.bqre35lordbvn4rtwtlign6no          stefanprodan/swarmprom-node-exporter:v0.16.0   node02.netology.yc   Running         Running 2 hours ago              
ojv8w351g946   swarm_monitoring_node-exporter.j69md7ol8z6bp5w3gqp61jfsw          stefanprodan/swarmprom-node-exporter:v0.16.0   node06.netology.yc   Running         Running 2 hours ago              
wqj4qmhcy9pj   swarm_monitoring_node-exporter.nba4ua0v5u7k7xh2upall2w8w          stefanprodan/swarmprom-node-exporter:v0.16.0   node04.netology.yc   Running         Running 2 hours ago              
ttm4ibo9a3l9   swarm_monitoring_node-exporter.qjmezayny3c6c5kaf8b6i8v5e          stefanprodan/swarmprom-node-exporter:v0.16.0   node01.netology.yc   Running         Running 2 hours ago              
2pdengznfhgp    \_ swarm_monitoring_node-exporter.qjmezayny3c6c5kaf8b6i8v5e      stefanprodan/swarmprom-node-exporter:v0.16.0   node01.netology.yc   Shutdown        Shutdown 2 hours ago             
76zv8unyj6yt   swarm_monitoring_node-exporter.w8a5dn2em5f85lsgviinp9v3z          stefanprodan/swarmprom-node-exporter:v0.16.0   node05.netology.yc   Running         Running 2 hours ago              
v5obh7bdh6ot   swarm_monitoring_node-exporter.zfbbdwqxrdzorocfb9kp92hfa          stefanprodan/swarmprom-node-exporter:v0.16.0   node03.netology.yc   Running         Running 2 hours ago              
olqx2n4x8jvv   swarm_monitoring_prometheus.1                                     stefanprodan/swarmprom-prometheus:v2.5.0       node03.netology.yc   Running         Running 2 hours ago              
wnmixxgpdcqg    \_ swarm_monitoring_prometheus.1                                 stefanprodan/swarmprom-prometheus:v2.5.0       node01.netology.yc   Shutdown        Shutdown 2 hours ago             
p7oudvj6zc2q   swarm_monitoring_unsee.1                                          cloudflare/unsee:v0.8.0                        node06.netology.yc   Running         Running 2 hours ago              
[root@node02 monitoring]# 

```
#### 8. Удаляем всё, чтобы не тратить деньги!
```bash
#docker destroy -auto-approve
```
