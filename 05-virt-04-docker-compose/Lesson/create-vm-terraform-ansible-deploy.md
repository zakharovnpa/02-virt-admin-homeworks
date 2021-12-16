## Выполнение Задачи №4*

### Создать вторую ВМ и подключить её к мониторингу развёрнутому на первом сервере.

#### План выполнения
- Подготовить Яндекс Облако
  - Удалить все ВМ
  - Удалить все сети и подсети
  - Проверить статус соединения с Яндекс Облаком утилитой yc
##### Порядок создания ВМ
- Запускаем создание ВМ, сети и подсети
```bash
terraform init

terrafirm validate

terraform plan

terraform apply -auto-approve
```
- Копируем в файл ` inventory ` ip внешний адрес созданной ВМ
 - Запускаем Playbook
```bash
ansible-playbook provision.yml 
```

Подсказка по этой задаче см. на 1 час 38 минут 17 секунд и га 1 час 41 минута 04 секунд от начала лекции
#### Первая фаза
1. В директории ./terraform скопирвать файл node01 в node02
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# cp node01.tf node02.tf 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# vim node02.tf 

```
2. Поменять в новом фале 01 на 02
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# cat node02.tf 
resource "yandex_compute_instance" "node02" {
  name                      = "node02"
  zone                      = "ru-central1-a"
  hostname                  = "node02.netology.cloud"
  allow_stopping_for_update = true

  resources {
    cores  = 8
    memory = 8
  }

  boot_disk {
    initialize_params {
      image_id    = "${var.centos-7-base}"
      name        = "root-node02"
      type        = "network-nvme"
      size        = "50"
    }
  }

  network_interface {
    subnet_id = "${yandex_vpc_subnet.default.id}"
    nat       = true
  }

  metadata = {
    ssh-keys = "centos:${file("~/.ssh/id_rsa.pub")}"
  }
}

```
Запустить терраформ
При этом создастся вторая виртуальная машина node02, но первая машина при этом удаляется
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# yc resource-manager folder list
+----------------------+---------------+--------+--------+
|          ID          |     NAME      | LABELS | STATUS |
+----------------------+---------------+--------+--------+
| b1ggdhpqn2g4ts7rsvfj | default       |        | ACTIVE |
| b1gd3hm4niaifoa8dahm | netology-alfa |        | ACTIVE |
+----------------------+---------------+--------+--------+

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/ansible# 
```

```tf

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of yandex-cloud/yandex from the dependency lock file
- Using previously-installed yandex-cloud/yandex v0.67.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```

```tf
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
Success! The configuration is valid.

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```

```tf
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform plan
yandex_vpc_subnet.default: Refreshing state... [id=e9bjuh1beitbgp5q3fb5]
yandex_vpc_network.default: Refreshing state... [id=enpg408972efls369k28]
yandex_compute_instance.node01: Refreshing state... [id=fhmklokig6f0516hc354]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply":

  # yandex_compute_instance.node01 has changed
  ~ resource "yandex_compute_instance" "node01" {
        id                        = "fhmklokig6f0516hc354"
      + labels                    = {}
        name                      = "node01"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }


Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan may include actions to undo or respond to these changes.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # yandex_compute_instance.node01 must be replaced
-/+ resource "yandex_compute_instance" "node01" {
      ~ created_at                = "2021-12-10T16:53:01Z" -> (known after apply)
      ~ folder_id                 = "b1gd3hm4niaifoa8dahm" -> (known after apply)
      ~ fqdn                      = "node01.netology.cloud" -> (known after apply)
      ~ hostname                  = "node01" -> "node01.netology.cloud" # forces replacement
      ~ id                        = "fhmklokig6f0516hc354" -> (known after apply)
      - labels                    = {} -> null
        name                      = "node01"
      + service_account_id        = (known after apply)
      ~ status                    = "running" -> (known after apply)
        # (5 unchanged attributes hidden)

      ~ boot_disk {
          ~ device_name = "fhm5p2n4o25qv9ba58mu" -> (known after apply)
          ~ disk_id     = "fhm5p2n4o25qv9ba58mu" -> (known after apply)
          ~ mode        = "READ_WRITE" -> (known after apply)
            # (1 unchanged attribute hidden)

          ~ initialize_params {
              + description = (known after apply)
                name        = "root-node01"
              + snapshot_id = (known after apply)
              ~ type        = "network-ssd" -> "network-nvme" # forces replacement
                # (2 unchanged attributes hidden)
            }
        }

      ~ network_interface {
          ~ index              = 0 -> (known after apply)
          ~ ip_address         = "192.168.101.27" -> (known after apply)
          ~ ipv6               = false -> (known after apply)
          + ipv6_address       = (known after apply)
          ~ mac_address        = "d0:0d:14:ae:29:28" -> (known after apply)
          ~ nat_ip_address     = "51.250.0.11" -> (known after apply)
          ~ nat_ip_version     = "IPV4" -> (known after apply)
          ~ security_group_ids = [] -> (known after apply)
            # (3 unchanged attributes hidden)
        }

      ~ placement_policy {
          + placement_group_id = (known after apply)
        }

      ~ resources {
          - gpus          = 0 -> null
            # (3 unchanged attributes hidden)
        }

      ~ scheduling_policy {
          ~ preemptible = false -> (known after apply)
        }
    }

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.cloud"
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
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = "e9bjuh1beitbgp5q3fb5"
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

Plan: 2 to add, 0 to change, 1 to destroy.

Changes to Outputs:
  ~ external_ip_address_node01_yandex_cloud = "51.250.0.11" -> (known after apply)
  ~ internal_ip_address_node01_yandex_cloud = "192.168.101.27" -> (known after apply)

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```
#### Запуск на выполнение
```tf
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform apply -auto-approve
yandex_vpc_network.default: Refreshing state... [id=enpg408972efls369k28]
yandex_vpc_subnet.default: Refreshing state... [id=e9bjuh1beitbgp5q3fb5]
yandex_compute_instance.node01: Refreshing state... [id=fhmklokig6f0516hc354]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply":

  # yandex_compute_instance.node01 has changed
  ~ resource "yandex_compute_instance" "node01" {
        id                        = "fhmklokig6f0516hc354"
      + labels                    = {}
        name                      = "node01"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }


Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan may include actions to undo or respond to these changes.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # yandex_compute_instance.node01 must be replaced
-/+ resource "yandex_compute_instance" "node01" {
      ~ created_at                = "2021-12-10T16:53:01Z" -> (known after apply)
      ~ folder_id                 = "b1gd3hm4niaifoa8dahm" -> (known after apply)
      ~ fqdn                      = "node01.netology.cloud" -> (known after apply)
      ~ hostname                  = "node01" -> "node01.netology.cloud" # forces replacement
      ~ id                        = "fhmklokig6f0516hc354" -> (known after apply)
      - labels                    = {} -> null
        name                      = "node01"
      + service_account_id        = (known after apply)
      ~ status                    = "running" -> (known after apply)
        # (5 unchanged attributes hidden)

      ~ boot_disk {
          ~ device_name = "fhm5p2n4o25qv9ba58mu" -> (known after apply)
          ~ disk_id     = "fhm5p2n4o25qv9ba58mu" -> (known after apply)
          ~ mode        = "READ_WRITE" -> (known after apply)
            # (1 unchanged attribute hidden)

          ~ initialize_params {
              + description = (known after apply)
                name        = "root-node01"
              + snapshot_id = (known after apply)
              ~ type        = "network-ssd" -> "network-nvme" # forces replacement
                # (2 unchanged attributes hidden)
            }
        }

      ~ network_interface {
          ~ index              = 0 -> (known after apply)
          ~ ip_address         = "192.168.101.27" -> (known after apply)
          ~ ipv6               = false -> (known after apply)
          + ipv6_address       = (known after apply)
          ~ mac_address        = "d0:0d:14:ae:29:28" -> (known after apply)
          ~ nat_ip_address     = "51.250.0.11" -> (known after apply)
          ~ nat_ip_version     = "IPV4" -> (known after apply)
          ~ security_group_ids = [] -> (known after apply)
            # (3 unchanged attributes hidden)
        }

      ~ placement_policy {
          + placement_group_id = (known after apply)
        }

      ~ resources {
          - gpus          = 0 -> null
            # (3 unchanged attributes hidden)
        }

      ~ scheduling_policy {
          ~ preemptible = false -> (known after apply)
        }
    }

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.cloud"
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
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = "e9bjuh1beitbgp5q3fb5"
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

Plan: 2 to add, 0 to change, 1 to destroy.

Changes to Outputs:
  ~ external_ip_address_node01_yandex_cloud = "51.250.0.11" -> (known after apply)
  ~ internal_ip_address_node01_yandex_cloud = "192.168.101.27" -> (known after apply)
yandex_compute_instance.node01: Destroying... [id=fhmklokig6f0516hc354]
yandex_compute_instance.node02: Creating...
yandex_compute_instance.node01: Still destroying... [id=fhmklokig6f0516hc354, 10s elapsed]
yandex_compute_instance.node02: Still creating... [10s elapsed]
yandex_compute_instance.node01: Destruction complete after 11s
yandex_compute_instance.node01: Creating...
yandex_compute_instance.node02: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node02: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node02: Creation complete after 40s [id=fhme8037t104b6ad2ker]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node01: Creation complete after 39s [id=fhmrtkbvjefibjbsiam9]

Apply complete! Resources: 2 added, 0 changed, 1 destroyed.

Outputs:

external_ip_address_node01_yandex_cloud = "51.250.11.110"
internal_ip_address_node01_yandex_cloud = "192.168.101.26"
```
#### После выполнения была удалена node01 и добавлена node02
```bash
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform plan
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 2, in output "internal_ip_address_node01_yandex_cloud":
│    2:   value = "${yandex_compute_instance.node01.network_interface.0.ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 6, in output "external_ip_address_node01_yandex_cloud":
│    6:   value = "${yandex_compute_instance.node01.network_interface.0.nat_ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 2, in output "internal_ip_address_node01_yandex_cloud":
│    2:   value = "${yandex_compute_instance.node01.network_interface.0.ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 6, in output "external_ip_address_node01_yandex_cloud":
│    6:   value = "${yandex_compute_instance.node01.network_interface.0.nat_ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 2, in output "internal_ip_address_node01_yandex_cloud":
│    2:   value = "${yandex_compute_instance.node01.network_interface.0.ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
╷
│ Error: Reference to undeclared resource
│ 
│   on output.tf line 6, in output "external_ip_address_node01_yandex_cloud":
│    6:   value = "${yandex_compute_instance.node01.network_interface.0.nat_ip_address}"
│ 
│ A managed resource "yandex_compute_instance" "node01" has not been declared in the root module.
╵
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# mc


root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
```

```tf
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
Success! The configuration is valid.

root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform plan
yandex_vpc_subnet.default: Refreshing state... [id=e9bjuh1beitbgp5q3fb5]
yandex_vpc_network.default: Refreshing state... [id=enpg408972efls369k28]
yandex_compute_instance.node01: Refreshing state... [id=fhmrtkbvjefibjbsiam9]
yandex_compute_instance.node02: Refreshing state... [id=fhme8037t104b6ad2ker]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply":

  # yandex_compute_instance.node01 has changed
  ~ resource "yandex_compute_instance" "node01" {
        id                        = "fhmrtkbvjefibjbsiam9"
      + labels                    = {}
        name                      = "node01"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }

  # yandex_compute_instance.node02 has changed
  ~ resource "yandex_compute_instance" "node02" {
        id                        = "fhme8037t104b6ad2ker"
      + labels                    = {}
        name                      = "node02"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }


Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan may include actions to undo or respond to these changes.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
  - destroy

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be destroyed
  # (because yandex_compute_instance.node01 is not in configuration)
  - resource "yandex_compute_instance" "node01" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T14:04:56Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node01.netology.cloud" -> null
      - hostname                  = "node01" -> null
      - id                        = "fhmrtkbvjefibjbsiam9" -> null
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
          - device_name = "fhm8e9s31p20aqrj45h4" -> null
          - disk_id     = "fhm8e9s31p20aqrj45h4" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node01" -> null
              - size     = 50 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.26" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:1b:ed:17:f9" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.11.110" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bjuh1beitbgp5q3fb5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 8 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node02 will be destroyed
  # (because yandex_compute_instance.node02 is not in configuration)
  - resource "yandex_compute_instance" "node02" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T14:04:46Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node02.netology.cloud" -> null
      - hostname                  = "node02" -> null
      - id                        = "fhme8037t104b6ad2ker" -> null
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
          - device_name = "fhm5buhclsm4l6kbm6cd" -> null
          - disk_id     = "fhm5buhclsm4l6kbm6cd" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node02" -> null
              - size     = 50 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.20" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:e4:00:67:e8" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.114.45" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bjuh1beitbgp5q3fb5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 8 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.cloud"
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
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = "e9bjuh1beitbgp5q3fb5"
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 2 to destroy.

Changes to Outputs:
  ~ external_ip_address_node01_yandex_cloud = "51.250.11.110" -> (known after apply)
  ~ internal_ip_address_node01_yandex_cloud = "192.168.101.26" -> (known after apply)

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform apply -auto-approve
yandex_vpc_network.default: Refreshing state... [id=enpg408972efls369k28]
yandex_vpc_subnet.default: Refreshing state... [id=e9bjuh1beitbgp5q3fb5]
yandex_compute_instance.node01: Refreshing state... [id=fhmrtkbvjefibjbsiam9]
yandex_compute_instance.node02: Refreshing state... [id=fhme8037t104b6ad2ker]

Note: Objects have changed outside of Terraform

Terraform detected the following changes made outside of Terraform since the last "terraform apply":

  # yandex_compute_instance.node01 has changed
  ~ resource "yandex_compute_instance" "node01" {
        id                        = "fhmrtkbvjefibjbsiam9"
      + labels                    = {}
        name                      = "node01"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }

  # yandex_compute_instance.node02 has changed
  ~ resource "yandex_compute_instance" "node02" {
        id                        = "fhme8037t104b6ad2ker"
      + labels                    = {}
        name                      = "node02"
        # (10 unchanged attributes hidden)





        # (5 unchanged blocks hidden)
    }


Unless you have made equivalent changes to your configuration, or ignored the relevant attributes using ignore_changes, the following plan may include actions to undo or respond to these changes.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create
  - destroy

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be destroyed
  # (because yandex_compute_instance.node01 is not in configuration)
  - resource "yandex_compute_instance" "node01" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T14:04:56Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node01.netology.cloud" -> null
      - hostname                  = "node01" -> null
      - id                        = "fhmrtkbvjefibjbsiam9" -> null
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
          - device_name = "fhm8e9s31p20aqrj45h4" -> null
          - disk_id     = "fhm8e9s31p20aqrj45h4" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node01" -> null
              - size     = 50 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.26" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:1b:ed:17:f9" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.11.110" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bjuh1beitbgp5q3fb5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 8 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node02 will be destroyed
  # (because yandex_compute_instance.node02 is not in configuration)
  - resource "yandex_compute_instance" "node02" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2021-12-11T14:04:46Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node02.netology.cloud" -> null
      - hostname                  = "node02" -> null
      - id                        = "fhme8037t104b6ad2ker" -> null
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
          - device_name = "fhm5buhclsm4l6kbm6cd" -> null
          - disk_id     = "fhm5buhclsm4l6kbm6cd" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node02" -> null
              - size     = 50 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.20" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:e4:00:67:e8" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.114.45" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bjuh1beitbgp5q3fb5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 8 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.cloud"
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
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = "e9bjuh1beitbgp5q3fb5"
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 2 to destroy.

Changes to Outputs:
  ~ external_ip_address_node01_yandex_cloud = "51.250.11.110" -> (known after apply)
  ~ internal_ip_address_node01_yandex_cloud = "192.168.101.26" -> (known after apply)
yandex_compute_instance.node01: Destroying... [id=fhmrtkbvjefibjbsiam9]
yandex_compute_instance.node02: Destroying... [id=fhme8037t104b6ad2ker]
yandex_compute_instance.node03: Creating...
yandex_compute_instance.node02: Still destroying... [id=fhme8037t104b6ad2ker, 10s elapsed]
yandex_compute_instance.node01: Still destroying... [id=fhmrtkbvjefibjbsiam9, 10s elapsed]
yandex_compute_instance.node03: Still creating... [10s elapsed]
yandex_compute_instance.node01: Destruction complete after 10s
yandex_compute_instance.node02: Destruction complete after 11s
yandex_compute_instance.node03: Still creating... [20s elapsed]
yandex_compute_instance.node03: Still creating... [30s elapsed]
yandex_compute_instance.node03: Still creating... [40s elapsed]
yandex_compute_instance.node03: Creation complete after 42s [id=fhm9pnogd629tf7ilmrn]

Apply complete! Resources: 1 added, 0 changed, 2 destroyed.

Outputs:

external_ip_address_node01_yandex_cloud = "62.84.113.235"
internal_ip_address_node01_yandex_cloud = "192.168.101.5"
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# 

```
#### Вторая фаза

6. А дальше надо из директории стек задеплоить два экспортера. В директории экспортерс есть отдельная конфигурация для этой задачи. Здесь всего два микросервиса. Один запускает нодеэкспортер и второй - сиадвизор
7. В конфигурации прометеуса.ямл добавить еще дае джобы, которые будут описывать нодеэкспортер и сиадвизор от второй виртуальной машины. Но только вместо имени надо будет добавить второй айпи адрес второй ВМ
8. Рестартануть микросервис под названием Прометеус
9. Зайти на первую ВМ в директорию опт/стек и выполнить команду докер-композ стоп прометеус и затем докер-композе ап -д. Так перезапустится прметеус с новым конфигом
