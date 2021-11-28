
# "5.2. Применение принципов IaaC в работе с виртуальными машинами" - Захаров Сергей Николаевич

## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.
- Какой из принципов IaaC является основополагающим?

**Ответ:**

1. Основные преимущества применения на практике IaaC паттернов:
- Паттерн IaaC значительно ускоряет процесс предоставления инфраструктуры для разработки, тестирования и масштабирования по мере необходимости. Все это повышает скорость  создания и вывода качественного продукта на рынок. 
- Обеспечение стабильности среды, устранение дрейфа конфигураций (произвольном изменении и обновлении конфигурации, несовпадению сред разработки, тестирования и развёртывания).
- Эффективная и быстрая разработка за счет упрощения предоставления инфраструктуры и повышения её консистентности. IaaC способствует ускорению каждого этапа жизненного цикла доставки ПО. У разработчиков появляется возможность быстро подготовить «песочницы» и среды непрерывной интеграции /непрерывного развёртывания (CI/CD), быстро предоставить  тестовые среды и инфраструктуру для проверки безопасности и удобства использования продукта.

2. Основополагающим принципом IaaC является идемпоте́нтность (лат.idem — тот же самый + potens — способный).
Это свойство объекта или операции, при повторном выполнении которой мы получаем результат идентичный предыдущему и всем последующим выполнениям.

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

**Ответ:**
1. Преимущества Ansible заключаются в том, что он быстро стартует на уже существующей инфраструктуре SSH. 
А также в том, что в Ansible применяется декларативный метод описания конфигураций. Ansible дегко расширяеется за счет быстрого подключения кастомных ролей и модулей.

2. Более надежным является метод push, т.к. это более безопасно с точки зрения поддержания правильной инфраструктуры (своевременная передача необходимых конфигураций).

## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

**Ответ:**

- Версия установенного VirtualBox на Windows 10
```md
C:\Program Files\Oracle\VirtualBox>virtualbox -help > vboxver.txt

C:\Program Files\Oracle\VirtualBox>type vboxver.txt
Oracle VM VirtualBox VM Selector v6.1.30
(C) 2005-2021 Oracle Corporation
All rights reserved.

No special options.

If you are looking for --startvm and related options, you need to use VirtualBoxVM.
```

- Версия установенного Vagrant на Windows 10
```md
C:\>vagrant -v
Vagrant 2.2.19
```

- Версия установенного Vagrant на Ubuntu-20.04 работающей в среде WSL
```md
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant --version
Vagrant 2.2.19
```

- Версия установенного Ansible на Ubuntu-20.04 работающей в среде WSL
```md
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.8.2 (default, Mar 13 2020, 10:14:16) [GCC 9.3.0]
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

- Создать виртуальную машину.
- Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
```
docker ps
```
**Ответ:**

- ВМ создана на ОС Windows 10, на которой установлены VirtualBox, Vagrant, запущена среда WSL (Windows Subsystem for Linux). В среде WSL запущена вторичная (виртуальная) ОС Ubuntu-20.04, в которой установлены Vagrant и Ansible. И затем, при помощи них создана ВМ **server1.netology**, на которой в процессе создания ВМ были установлены Git, Curl, Docker.
  [Описание процесса инсталляции виртуальной ОС Ubuntu-20.04 на WSL](https://github.com/zakharovnpa/02-virt-admin-homeworks/blob/main/05-virt-02-iaac/install-wsl2%2Bvagrant/Install.md)
- На виртуальной Ubuntu-20.04 установлены Vagrant, ansible. Создана ВМ **server1.netology** и в ней запущены curl, git, docker
  [Описание процесса создания ВМ server1.netology и инсталляции curl, git, docker](https://github.com/zakharovnpa/02-virt-admin-homeworks/blob/main/05-virt-02-iaac/Install-ansible/Install-on-Ubuntu-20-ansible.md)

- Установленный Docker в ВМ server1.netology
```md
root@server1:~# docker --version
Docker version 20.10.11, build dea9396

root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```
