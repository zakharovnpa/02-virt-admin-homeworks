# "5.4. Оркестрация группой Docker контейнеров на примере Docker Compose" - Захаров Сергей Николаевич

## Задача 1

Создать собственный образ операционной системы с помощью Packer.

Для получения зачета, вам необходимо предоставить:
- Скриншот страницы, как на слайде из презентации (слайд 37).

**Ответ:**
Создан новый ![образ](/05-virt-04-docker-compose/img/new-images-in-yandex-cloud.png)

## Задача 2

Создать вашу первую виртуальную машину в Яндекс.Облаке.

Для получения зачета, вам необходимо предоставить:
- Скриншот страницы свойств созданной ВМ, как на примере ниже:


<p align="center">
  <img width="1200" height="600" src="./img/yc_01.png">
</p>

**Ответ:**

![yc-compute-image-list](/05-virt-04-docker-compose/img/yc-compute-image-list.png)
![running-node01](/05-virt-04-docker-compose/img/running-node01.png)


## Задача 3

Создать ваш первый готовый к боевой эксплуатации компонент мониторинга, состоящий из стека микросервисов.

Для получения зачета, вам необходимо предоставить:
- Скриншот работающего веб-интерфейса Grafana с текущими метриками, как на примере ниже
<p align="center">
  <img width="1200" height="600" src="./img/yc_02.png">
</p>

**Ответ:**
![running-grafana](/05-virt-04-docker-compose/img/running-grafana.png)

![running-prometheus](/05-virt-04-docker-compose/img/running-prometheus.png)

## Задача 4 (*)

Создать вторую ВМ и подключить её к мониторингу развёрнутому на первом сервере.

Для получения зачета, вам необходимо предоставить:
- Скриншот из Grafana, на котором будут отображаться метрики добавленного вами сервера.

**Ответ:**
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
При этом создастся вторая виртуальная машина node02
#### Вторая фаза

6. А дальше надо из директории стек задеплоить два экспортера. В директории экспортерс есть отдельная конфигурация для этой задачи. Здесь всего два микросервиса. Один запускает нодеэкспортер и второй - сиадвизор
7. В конфигурации прометеуса.ямл добавить еще дае джобы, которые будут описывать нодеэкспортер и сиадвизор от второй виртуальной машины. Но только вместо имени надо будет добавить второй айпи адрес второй ВМ
8. Рестартануть микросервис под названием Прометеус
9. Зайти на первую ВМ в директорию опт/стек и выполнить команду докер-композ стоп прометеус и затем докер-композе ап -д. Так перезапустится прметеус с новым конфигом
