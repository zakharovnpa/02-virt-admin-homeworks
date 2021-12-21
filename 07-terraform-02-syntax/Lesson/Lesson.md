## Выполнение домашнего задания по теме "7.3 Облачные провайдеры и синтаксис Терраформ"

### Работаем в Яндекс.Облаке. Будем создавать ВМ с помощью настройки файла terraform ` main.tf `[Resource yandex_compute_image](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/compute_image)

#### 1. Готовим переменные окружения для сохранения токена доступа к облаку в системе. [Статья](https://cloud.yandex.com/en-ru/docs/iam/operations/iam-token/create)
Пример:
```bash
Использование токена IAM, полученного через интерфейс командной строки
Сохраните токен IAM в переменной в интерфейсе командной строки и используйте его в других запросах из командной строки. Пример запроса на получение списка облаков:
```
```bash
$ export IAM_TOKEN=`yc iam create-token`
$ curl -H "Authorization: Bearer ${IAM_TOKEN}" \
    https://resource-manager.api.cloud.yandex.net/resource-manager/v1/clouds
```
    
Получите токен IAM:
```bash
$ yc iam create-token
Укажите полученный IAM-токен при доступе к ресурсам Яндекс.Облака через API. Передайте токен IAM в Authorizationзаголовке в следующем формате:

Authorization: Bearer <IAM-TOKEN>    
```

#### 2. Как выбрать необходимый образ диска из доступных

```bash
yc compute image list --folder-id standard-images
```
#### 3. Создаем главный файл конфигурации terraform ` main.tf ` [по статье](https://cloud.yandex.ru/docs/solutions/infrastructure-management/terraform-quickstart)

    Создайте новую директорию с произвольным названием, например ` yandex-cloud-terraform `. 
    В ней будут храниться конфигурационные файлы и сохраненные состояния Terraform и инфраструктуры.
    
```bash
mkdir -p yandex-cloud-terraform 
```
Создаем файл конфигурации terraform ` main.tf `

```bash
# В начале конфигурационного файла необходимо задать настройки провайдера.

terraform {
  required_providers {
    yandex = {
      source  = "yandex-cloud/yandex"   # глобальный адрес источника провайдера.
      version = "0.61.0"                # минимальная версия провайдера, с которой совместим модуль. 
                                        # Номер версии можно посмотреть на странице провайдера (кнопка USE PROVIDER в верхнем правом углу).
         
           
    }
  }
}

provider "yandex" {                               # название провайдера
  token     = "<OAuth>"                           # OAuth-токен для доступа к Yandex.Cloud.
  cloud_id  = "<идентификатор облака>"            # идентификатор облака, в котором Terraform создаст ресурсы.
  folder_id = "<идентификатор каталога>"          # идентификатор каталога, в котором по умолчанию будут создаваться ресурсы.
  zone      = "<зона доступности по умолчанию>"   # зона доступности, в которой по умолчанию будут создаваться все облачные ресурсы.
}

```
#### 4. Подготовьте план инфраструктуры

С помощью Terraform в Yandex.Cloud можно создавать облачные ресурсы всех типов: виртуальные машины, диски, образы и т.д. Подробную информацию о ресурсах, создающихся с помощью Terraform, см. в [документации провайдера](https://www.terraform.io/docs/providers/yandex/index.html).

Для создания ресурса необходимо указать набор обязательных и опциональных параметров, определяющих свойства ресурса. Такие описания ресурсов составляют план инфраструктуры.

1. По плану будут созданы следующие ресурсы:
- Облачная сеть ` network-1 ` с подсетью ` subnet-1 ` в зоне доступности ` ru-central1-a `.
- Две виртуальные машины Linux: 
  - ` terraform1 ` (2 ядра и 2 Гб оперативной памяти) и 
  - ` terraform2 ` (4 ядра и 4 Гб оперативной памяти). 
  
  Они автоматически получат публичные и приватные IP-адреса из диапазона 192.168.10.0/24 в подсети ` subnet-1 `.
  
  2. Сгенерируйте пару SSH-ключей для доступа к ВМ по SSH.


В конфигурации виртуальной машины вам потребуется указать идентификатор образа загрузочного диска. Список доступных публичных образов можно получить командой CLI 
```bash
yc compute image list --folder-id standard-images
```
3. Опишите параметры ресурсов в файле main.tf:

    В параметре ssh-keys блока metadata укажите путь к публичной части SSH ключа.
    В image_id задайте идентификатор образа загрузочного диска.

4. файл ` main.tf `

```hcl
<настройки провайдера>

resource "yandex_compute_instance" "vm-1" {
  name = "terraform1"

  resources {
    cores  = 2
    memory = 2
  }

  boot_disk {
    initialize_params {
      image_id = "fd87va5cc00gaq2f5qfb"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }

  metadata = {
    ssh-keys = "ubuntu:${file("~/.ssh/id_rsa.pub")}"
  }
}

resource "yandex_compute_instance" "vm-2" {
  name = "terraform2"

  resources {
    cores  = 4
    memory = 4
  }

  boot_disk {
    initialize_params {
      image_id = "fd87va5cc00gaq2f5qfb"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }

  metadata = {
    ssh-keys = "ubuntu:${file("~/.ssh/id_rsa.pub")}"
  }
}

resource "yandex_vpc_network" "network-1" {
  name = "network1"
}

resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-a"
  network_id     = yandex_vpc_network.network-1.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

output "internal_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.ip_address
}

output "internal_ip_address_vm_2" {
  value = yandex_compute_instance.vm-2.network_interface.0.ip_address
}


output "external_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.nat_ip_address
}

output "external_ip_address_vm_2" {
  value = yandex_compute_instance.vm-2.network_interface.0.nat_ip_address
}

```

Конфигурации ресурсов задаются сразу после конфигурации провайдера:
```hcl
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
}

provider "yandex" {
  token     = "OAuth_token"
  cloud_id  = "cloud-id"
  folder_id = "folder-id"
  zone      = "ru-central1-a"
}

resource "yandex_compute_instance" "vm-1" {
  name = "terraform1"
}
```

```hcl
module "news" {
  source = "../modules/instance"

  subnet_id     = "${var.yc_subnet_id}"
  image         = "centos-8"
  platform_id   = "standard-v2"
  name          = "news"
  description   = "News App Demo"
  instance_role = "news,balancer"
  users         = "centos"
  cores         = "2"
  boot_disk     = "network-ssd"
  disk_size     = "20"
  nat           = "true"
  memory        = "2"
  core_fraction = "100"
}

```
