
# "5.2. Применение принципов IaaC в работе с виртуальными машинами" - Захаров Сергей Николаевич

## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.
- Какой из принципов IaaC является основополагающим?

**Ответ:**

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

**Ответ:**

## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

**Ответ:**

- Версия установенного VirtualBox
```md
C:\Program Files\Oracle\VirtualBox>virtualbox -help > vboxver.txt

C:\Program Files\Oracle\VirtualBox>type vboxver.txt
Oracle VM VirtualBox VM Selector v6.1.30
(C) 2005-2021 Oracle Corporation
All rights reserved.

No special options.

If you are looking for --startvm and related options, you need to use VirtualBoxVM.
```

- Версия установенного Vagrant в Windows 10
```md
C:\>vagrant -v
Vagrant 2.2.19
```

- Версия установенного Vagrant в Ubuntu-20.04 на WSL
```md
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant --version
Vagrant 2.2.19
```

- Версия установенного Ansible
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
- ВМ создана на ПК с Windows 10, на котором установлен VirtualBox, Vagrant, запущен WSL (Windows-Service-Linux) и в нем запущена вторичная (витруальная) ОС Ubuntu-20.04. 
  [Логи процесса инсталляции](https://github.com/zakharovnpa/02-virt-admin-homeworks/blob/main/05-virt-02-iaac/install-wsl2%2Bvagrant/Install.md)
- На виртуальной Ubuntu-20.04 установлены Vagrant, ansible, curl, git, docker
  [Логи процесса инсталляции](https://github.com/zakharovnpa/02-virt-admin-homeworks/blob/main/05-virt-02-iaac/Install-ansible/Install-on-Ubuntu-20-ansible.md)

- Установленный Docker в ВМ server1.netology
```md
root@server1:~# docker --version
Docker version 20.10.11, build dea9396

root@server1:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```
