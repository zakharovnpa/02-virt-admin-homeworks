## Шаг 1. На ПК Sergey-PC установка Virtualbox, Vagrant, запуска WSL и одновременно с ней запуск компонента ОС Linux.

### Запуск PowerShell и просмотр состояния WSL
```yml
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)

PS C:\Windows\system32>
```
```yml
PS C:\Windows\system32> wsl --version

(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Использование: wsl.exe [Аргумент]

Аргументы:

    --install <Параметры>
        Установите компоненты подсистемы Windows для Linux. Если параметры не указаны,
        рекомендуемые компоненты будут установлены вместе с распределением по умолчанию.

        Чтобы просмотреть распределение по умолчанию и список других допустимых распределений,
        используйте команду 'wsl --list --online'.

        Параметры:
            --distribution, -d [Аргумент]
                Указывает распределение для загрузки и установки по имени.

                Аргументы:
                    Допустимое имя распределения (без учета регистра).

                Примеры:
                    wsl --install -d Ubuntu
                    wsl --install --distribution Debian

    --list, -l [Параметры]
        Перечисление распределений.

        Параметры:
            --online, -o
                Отображение списка доступных распределений для установки с помощью команды 'wsl --install'.

    --help
        Вывод сведений об использовании.
PS C:\Windows\system32>
```
### Доступные дистрибутивы
```yml
PS C:\Windows\system32> wsl -l -o
Ниже приведен список допустимых распределений, которые можно установить.
Распределение по умолчанию помечено знаком «*».
Установите с помощью команды wsl --install -d <Distro>

  NAME            FRIENDLY NAME
* Ubuntu          Ubuntu
  Debian          Debian GNU/Linux
  kali-linux      Kali Linux Rolling
  openSUSE-42     openSUSE Leap 42
  SLES-12         SUSE Linux Enterprise Server v12
  Ubuntu-16.04    Ubuntu 16.04 LTS
  Ubuntu-18.04    Ubuntu 18.04 LTS
  Ubuntu-20.04    Ubuntu 20.04 LTS
PS C:\Windows\system32>
PS C:\Windows\system32>
```
### Малый вариант вывода команды ` wsl -l -v `, т.к. WSL не установлена
```yml
PS C:\Windows\system32> wsl -l -v

(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Использование: wsl.exe [Аргумент]

Аргументы:

    --install <Параметры>
        Установите компоненты подсистемы Windows для Linux. Если параметры не указаны,
        рекомендуемые компоненты будут установлены вместе с распределением по умолчанию.

        Чтобы просмотреть распределение по умолчанию и список других допустимых распределений,
        используйте команду 'wsl --list --online'.

        Параметры:
            --distribution, -d [Аргумент]
                Указывает распределение для загрузки и установки по имени.

                Аргументы:
                    Допустимое имя распределения (без учета регистра).

                Примеры:
                    wsl --install -d Ubuntu
                    wsl --install --distribution Debian

    --list, -l [Параметры]
        Перечисление распределений.

        Параметры:
            --online, -o
                Отображение списка доступных распределений для установки с помощью команды 'wsl --install'.

    --help
        Вывод сведений об использовании.
PS C:\Windows\system32>
```
### Сбор сведений о системе
```yml
PS C:\Windows\system32> systeminfo

Имя узла:                         DESKTOP-LTI9L04
Название ОС:                      Майкрософт Windows 10 Домашняя
Версия ОС:                        10.0.19044 Н/Д построение 19044
Изготовитель ОС:                  Microsoft Corporation
Параметры ОС:                     Изолированная рабочая станция
Сборка ОС:                        Multiprocessor Free
Зарегистрированный владелец:      serjent@yandex.ru
Зарегистрированная организация:
Код продукта:                     00326-10000-00000-AA293
Дата установки:                   03.12.2021, 23:55:37
Время загрузки системы:           03.12.2021, 22:55:16
Изготовитель системы:             System manufacturer
Модель системы:                   System Product Name
Тип системы:                      x64-based PC
Процессор(ы):                     Число процессоров - 1.
                                  [01]: AMD64 Family 16 Model 10 Stepping 0 AuthenticAMD ~3000 МГц
Версия BIOS:                      American Megatrends Inc. 3029   , 05.07.2012
Папка Windows:                    C:\Windows
Системная папка:                  C:\Windows\system32
Устройство загрузки:              \Device\HarddiskVolume1
Язык системы:                     ru;Русский
Язык ввода:                       ru;Русский
Часовой пояс:                     (UTC+03:00) Москва, Санкт-Петербург
Полный объем физической памяти:   16 382 МБ
Доступная физическая память:      12 987 МБ
Виртуальная память: Макс. размер: 19 326 МБ
Виртуальная память: Доступна:     15 951 МБ
Виртуальная память: Используется: 3 375 МБ
Расположение файла подкачки:      C:\pagefile.sys
Домен:                            WORKGROUP
Сервер входа в сеть:              \\WIN-QQKK3621T95
Исправление(я):                   Число установленных исправлений - 4.
                                  [01]: KB5004331
                                  [02]: KB5003791
                                  [03]: KB5006670
                                  [04]: KB5005699
Сетевые адаптеры:                 Число сетевых адаптеров - 2.
                                  [01]: Realtek PCIe GbE Family Controller
                                        Имя подключения: Ethernet
                                        Состояние:       Носитель отключен
                                  [02]: Qualcomm Atheros AR922X Wireless Network Adapter
                                        Имя подключения: Беспроводная сеть
                                        DHCP включен:    Да
                                        DHCP-сервер:     192.168.1.1
                                        IP-адрес
                                        [01]: 192.168.1.22
                                        [02]: fe80::c0e0:64e8:1978:1dd8
Требования Hyper-V:               Расширения режима мониторинга виртуальной машины: Да
                                  Виртуализация включена во встроенном ПО: Да
                                  Преобразование адресов второго уровня: Да
                                  Доступно предотвращение выполнения данных: Да
PS C:\Windows\system32>
```
### Отключенные компоненты Windows системы виртуализации

![Отключенные компоненты Windows системы виртуализации](/05-virt-02-iaac/install-wsl2+vagrant/img/windows-virtual-components.PNG)
### Подготовка к установке WSL
#### Статья [Установка WSL](https://docs.microsoft.com/ru-ru/windows/wsl/install)
### Установка VirtualBox
#### Скачиваем последний актуальный дистрибутив [со страницы загрузки](https://www.virtualbox.org/wiki/Downloads)
#### Запускаем и устанавливаем VirtualBox
#### Скачиваем Vagrant [со страницы загрузки](https://www.vagrantup.com/downloads). Пока не устанавливаем.
#### Запускаем установку WSL и дистрибутива Ubuntu-20.04
```yml
PS C:\Windows\system32> wsl --install -d Ubuntu-20.04
Выполняется установка: Платформа виртуальной машины
Установка "Платформа виртуальной машины" выполнена.
Выполняется установка: Подсистема Windows для Linux
Установка "Подсистема Windows для Linux" выполнена.
Загрузка: Ядро WSL
Выполняется установка: Ядро WSL
Установка "Ядро WSL" выполнена.
Загрузка: Ubuntu 20.04 LTS
[=======                   13,2%                           ]
Требуемая операция выполнена успешно. Чтобы сделанные изменения вступили в силу, следует перезагрузить систему.
PS C:\Windows\system32>
```
#### Статус WSL после установки до перезагрузки Windows
```yml
PS C:\Windows\system32> wsl --status

(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Использование: wsl.exe [Аргумент]

Аргументы:

    --install <Параметры>
        Установите компоненты подсистемы Windows для Linux. Если параметры не указаны,
        рекомендуемые компоненты будут установлены вместе с распределением по умолчанию.

        Чтобы просмотреть распределение по умолчанию и список других допустимых распределений,
        используйте команду 'wsl --list --online'.

        Параметры:
            --distribution, -d [Аргумент]
                Указывает распределение для загрузки и установки по имени.

                Аргументы:
                    Допустимое имя распределения (без учета регистра).

                Примеры:
                    wsl --install -d Ubuntu
                    wsl --install --distribution Debian

    --list, -l [Параметры]
        Перечисление распределений.

        Параметры:
            --online, -o
                Отображение списка доступных распределений для установки с помощью команды 'wsl --install'.

    --help
        Вывод сведений об использовании.
PS C:\Windows\system32>
```
#### После перезагрузки Windows
##### Автоматически открылось окно запроса на создание пользователя в Ubuntu
```yml
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: maestro
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.10.16.3-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Dec  4 11:59:51 +04 2021

  System load:  0.05               Processes:             8
  Usage of /:   0.4% of 250.98GB   Users logged in:       0
  Memory usage: 0%                 IPv4 address for eth0: 172.17.50.213
  Swap usage:   0%

0 updates can be installed immediately.
0 of these updates are security updates.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


This message is shown once once a day. To disable it please create the
/home/maestro/.hushlogin file.
maestro@DESKTOP-LTI9L04:~$ sudo -i
[sudo] password for maestro:
Welcome to Ubuntu 20.04 LTS (GNU/Linux 5.10.16.3-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Dec  4 12:01:17 +04 2021

  System load:  0.05               Processes:             10
  Usage of /:   0.4% of 250.98GB   Users logged in:       0
  Memory usage: 0%                 IPv4 address for eth0: 172.17.50.213
  Swap usage:   0%

0 updates can be installed immediately.
0 of these updates are security updates.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


This message is shown once once a day. To disable it please create the
/root/.hushlogin file.
root@DESKTOP-LTI9L04:~#
root@DESKTOP-LTI9L04:~# type mc
-bash: type: mc: not found
root@DESKTOP-LTI9L04:~#
```
![Создание пользователя и вход в систему Ubuntu](/05-virt-02-iaac/install-wsl2+vagrant/img/Ubuntu-installing.PNG)
##### Состояние службы WSL
```yml
PS C:\Windows\system32> wsl --status
Распределение по умолчанию: Ubuntu-20.04
Версия по умолчанию: 2

Подсистема Windows для Linux в последний раз обновлена 04.12.2021
Ядро подсистемы Windows для Linux можно обновить вручную с помощью команды wsl --update, но автоматическое обновление невозможно из-за параметров системы.
Чтобы получать автоматические обновления ядра, включите параметр центра обновления Windows: «Получение обновлений для других продуктов Майкрософт при обновлении Windows».
Дополнительные сведения см. на странице https://aka.ms/wsl2kernel.

Версия ядра: 5.10.16
PS C:\Windows\system32>
PS C:\Windows\system32> wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-20.04    Running         2
PS C:\Windows\system32>
PS C:\Windows\system32>
```
##### Состояние дополнительных компонентов Windows
![Добавленные компоненты](/05-virt-02-iaac/install-wsl2+vagrant/img/windows-virtual-components-update.PNG)
##### Системинфо показывает изменения в разделе "Требования Hyper-V"
```yml
PS C:\Windows\system32> systeminfo

Имя узла:                         DESKTOP-LTI9L04
Название ОС:                      Майкрософт Windows 10 Домашняя
Версия ОС:                        10.0.19044 Н/Д построение 19044
Изготовитель ОС:                  Microsoft Corporation
Параметры ОС:                     Изолированная рабочая станция
Сборка ОС:                        Multiprocessor Free
Зарегистрированный владелец:      serjent@yandex.ru
Зарегистрированная организация:
Код продукта:                     00326-10000-00000-AA293
Дата установки:                   04.12.2021, 0:55:37
Время загрузки системы:           04.12.2021, 11:49:26
Изготовитель системы:             System manufacturer
Модель системы:                   System Product Name
Тип системы:                      x64-based PC
Процессор(ы):                     Число процессоров - 1.
                                  [01]: AMD64 Family 16 Model 10 Stepping 0 AuthenticAMD ~3000 МГц
Версия BIOS:                      American Megatrends Inc. 3029   , 05.07.2012
Папка Windows:                    C:\Windows
Системная папка:                  C:\Windows\system32
Устройство загрузки:              \Device\HarddiskVolume1
Язык системы:                     ru;Русский
Язык ввода:                       ru;Русский
Часовой пояс:                     (UTC+04:00) Ижевск, Самара
Полный объем физической памяти:   16 382 МБ
Доступная физическая память:      12 495 МБ
Виртуальная память: Макс. размер: 19 326 МБ
Виртуальная память: Доступна:     15 363 МБ
Виртуальная память: Используется: 3 963 МБ
Расположение файла подкачки:      C:\pagefile.sys
Домен:                            WORKGROUP
Сервер входа в сеть:              \\DESKTOP-LTI9L04
Исправление(я):                   Число установленных исправлений - 5.
                                  [01]: KB5006365
                                  [02]: KB5003791
                                  [03]: KB5007186
                                  [04]: KB5006753
                                  [05]: KB5005699
Сетевые адаптеры:                 Число сетевых адаптеров - 4.
                                  [01]: Realtek PCIe GbE Family Controller
                                        Имя подключения: Ethernet
                                        Состояние:       Носитель отключен
                                  [02]: Qualcomm Atheros AR922X Wireless Network Adapter
                                        Имя подключения: Беспроводная сеть
                                        DHCP включен:    Да
                                        DHCP-сервер:     192.168.1.1
                                        IP-адрес
                                        [01]: 192.168.1.22
                                        [02]: fe80::c0e0:64e8:1978:1dd8
                                  [03]: VirtualBox Host-Only Ethernet Adapter
                                        Имя подключения: VirtualBox Host-Only Network
                                        DHCP включен:    Нет
                                        IP-адрес
                                        [01]: 192.168.56.1
                                        [02]: fe80::8d07:337f:8722:1386
                                  [04]: Hyper-V Virtual Ethernet Adapter
                                        Имя подключения: vEthernet (WSL)
                                        DHCP включен:    Нет
                                        IP-адрес
                                        [01]: 172.17.48.1
                                        [02]: fe80::7144:2dce:6c37:462e
Требования Hyper-V:               Обнаружена низкоуровневая оболочка. Функции, необходимые для Hyper-V, отображены не будут.
PS C:\Windows\system32>
```
## Шаг 2. На ПК Sergey-PC установка на ОС Ubuntu-20.04 утилит Vagrant и Midnight Commander
### Устанавливаем Vagrant внутри Linux на WSL по [мануалу](https://www.vagrantup.com/docs/other/wsl)
```yml
# run inside WSL 2
# check https://www.vagrantup.com/downloads for more info
```
#### Устанавливаем ключ для подключеня репозитория Hasicorp
```ps
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```
#### Подключаем репозиторий Hasicorp
```ps
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```
##### Результат
```ps
root@DESKTOP-LTI9L04:~#
root@DESKTOP-LTI9L04:~# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
root@DESKTOP-LTI9L04:~#
root@DESKTOP-LTI9L04:~# apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:2 https://apt.releases.hashicorp.com focal InRelease [9495 B]
Get:3 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:4 https://apt.releases.hashicorp.com focal/main amd64 Packages [37.8 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [970 kB]
Get:8 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1062 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/main Translation-en [506 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal/main amd64 c-n-f Metadata [29.5 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages [8628 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [196 kB]
Get:13 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [9076 B]
Get:14 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [560 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [80.2 kB]
Get:16 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 c-n-f Metadata [528 B]
Get:17 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [663 kB]
Get:18 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [111 kB]
Get:19 http://archive.ubuntu.com/ubuntu focal/universe Translation-en [5124 kB]
Get:20 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [12.9 kB]
Get:21 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [21.9 kB]
Get:22 http://security.ubuntu.com/ubuntu focal-security/multiverse Translation-en [4948 B]
Get:23 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 c-n-f Metadata [540 B]
Get:24 http://archive.ubuntu.com/ubuntu focal/universe amd64 c-n-f Metadata [265 kB]
Get:25 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [144 kB]
Get:26 http://archive.ubuntu.com/ubuntu focal/multiverse Translation-en [104 kB]
Get:27 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 c-n-f Metadata [9136 B]
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1386 kB]
Get:29 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [281 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [14.6 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [606 kB]
Get:32 http://archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [86.8 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 c-n-f Metadata [528 B]
Get:34 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [877 kB]
Get:35 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [190 kB]
Get:36 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [19.6 kB]
Get:37 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [24.8 kB]
Get:38 http://archive.ubuntu.com/ubuntu focal-updates/multiverse Translation-en [6928 B]
Get:39 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 c-n-f Metadata [616 B]
Get:40 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [41.2 kB]
Get:41 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [9732 B]
Get:42 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [516 B]
Get:43 http://archive.ubuntu.com/ubuntu focal-backports/restricted amd64 c-n-f Metadata [116 B]
Get:44 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [18.9 kB]
Get:45 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [7524 B]
Get:46 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [644 B]
Get:47 http://archive.ubuntu.com/ubuntu focal-backports/multiverse amd64 c-n-f Metadata [116 B]
Fetched 22.7 MB in 8s (2763 kB/s)
Reading package lists... Done
root@DESKTOP-LTI9L04:~#
```
#### Обновляем установщики
```yml
apt-get update
```
##### Результат
```yml
root@DESKTOP-LTI9L04:~#
root@DESKTOP-LTI9L04:~# apt-get update
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Hit:3 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:4 https://apt.releases.hashicorp.com focal InRelease
Get:5 http://archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Fetched 222 kB in 1s (266 kB/s)
Reading package lists... Done
```
#### Запускаем установку Vagrant
```yml
apt-get install vagrant
```
##### Результат
```yml
root@DESKTOP-LTI9L04:~# apt-get install vagrant
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  vagrant
0 upgraded, 1 newly installed, 0 to remove and 251 not upgraded.
Need to get 41.5 MB of archives.
After this operation, 117 MB of additional disk space will be used.
Get:1 https://apt.releases.hashicorp.com focal/main amd64 vagrant amd64 2.2.19 [41.5 MB]
71% [1 vagrant 37.0 MB/41.5 MB 89%]                                                                        2446 kB/s 1s
```
```yml
Fetched 41.5 MB in 20s (2103 kB/s)
Selecting previously unselected package vagrant.
(Reading database ... 31836 files and directories currently installed.)
Preparing to unpack .../vagrant_2.2.19_amd64.deb ...
Unpacking vagrant (2.2.19) ...
Setting up vagrant (2.2.19) ...
root@DESKTOP-LTI9L04:~#

```
#### Смотрим версию vagrant
```yml
root@DESKTOP-LTI9L04:~# vagrant --version
Vagrant 2.2.19
```
### Устанавливаем утилиту Midnight Commander
```yml
apt install mc
```
```ps
root@DESKTOP-LTI9L04:~# apt install mc
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libssh2-1 mc-data unzip
Suggested packages:
  arj catdvi | texlive-binaries dbview djvulibre-bin epub-utils genisoimage gv imagemagick libaspell-dev links | w3m
  | lynx odt2txt poppler-utils python python-boto python-tz xpdf | pdf-viewer zip
The following NEW packages will be installed:
  libssh2-1 mc mc-data unzip
0 upgraded, 4 newly installed, 0 to remove and 251 not upgraded.
Need to get 1986 kB of archives.
After this operation, 8587 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal/universe amd64 libssh2-1 amd64 1.8.0-2.1build1 [75.4 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/universe amd64 mc-data all 3:4.8.24-2ubuntu1 [1265 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/universe amd64 mc amd64 3:4.8.24-2ubuntu1 [477 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/main amd64 unzip amd64 6.0-25ubuntu1 [169 kB]
Fetched 1986 kB in 1s (1622 kB/s)
Selecting previously unselected package libssh2-1:amd64.
(Reading database ... 38154 files and directories currently installed.)
Preparing to unpack .../libssh2-1_1.8.0-2.1build1_amd64.deb ...
Unpacking libssh2-1:amd64 (1.8.0-2.1build1) ...
Selecting previously unselected package mc-data.
Preparing to unpack .../mc-data_3%3a4.8.24-2ubuntu1_all.deb ...
Unpacking mc-data (3:4.8.24-2ubuntu1) ...
Selecting previously unselected package mc.
Preparing to unpack .../mc_3%3a4.8.24-2ubuntu1_amd64.deb ...
Unpacking mc (3:4.8.24-2ubuntu1) ...
Selecting previously unselected package unzip.
Preparing to unpack .../unzip_6.0-25ubuntu1_amd64.deb ...
Unpacking unzip (6.0-25ubuntu1) ...
Setting up unzip (6.0-25ubuntu1) ...
Setting up mc-data (3:4.8.24-2ubuntu1) ...
Setting up libssh2-1:amd64 (1.8.0-2.1build1) ...
Setting up mc (3:4.8.24-2ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9) ...
root@DESKTOP-LTI9L04:~#
```
### Шаг 3. Создание директории проектов для будущих ВМ, запускаемых с помощью Vagrant
#### Переходим в домашнй каталог поьзователя Windows, в УЗ которого запущен WSL
```cmd
root@DESKTOP-LTI9L04:~# pwd
/root
root@DESKTOP-LTI9L04:~#
root@DESKTOP-LTI9L04:~# cd /mnt/c/Users/serje/
root@DESKTOP-LTI9L04:/mnt/c/Users/serje#
root@DESKTOP-LTI9L04:/mnt/c/Users/serje# pwd
/mnt/c/Users/serje
```
```cmd
root@DESKTOP-LTI9L04:/mnt/c/Users/serje# ls -lha
total 3.7M
drwxrwxrwx 1 root root  512 Dec  4 11:05  .
dr-xr-xr-x 1 root root  512 Dec  4 00:20  ..
drwxrwxrwx 1 root root  512 Dec  4 11:31  .VirtualBox
drwxrwxrwx 1 root root  512 Dec  4 00:03 '3D Objects'
drwxrwxrwx 1 root root  512 Dec  4 00:01  AppData
lrwxrwxrwx 1 root root   34 Dec  4 00:01 'Application Data' -> /mnt/c/Users/serje/AppData/Roaming
drwxrwxrwx 1 root root  512 Dec  4 00:03  Contacts
lrwxrwxrwx 1 root root   62 Dec  4 00:01  Cookies -> /mnt/c/Users/serje/AppData/Local/Microsoft/Windows/INetCookies
drwxrwxrwx 1 root root  512 Dec  4 00:05  Documents
drwxrwxrwx 1 root root  512 Dec  4 11:10  Downloads
drwxrwxrwx 1 root root  512 Dec  4 00:07  Favorites
drwxrwxrwx 1 root root  512 Dec  4 00:03  Links
lrwxrwxrwx 1 root root   32 Dec  4 00:01 'Local Settings' -> /mnt/c/Users/serje/AppData/Local
drwxrwxrwx 1 root root  512 Dec  4 00:03  Music
-rwxrwxrwx 1 root root 1.5M Dec  4 11:47  NTUSER.DAT
-rwxrwxrwx 1 root root  64K Dec  4 00:01  NTUSER.DAT{53b39e88-18c4-11ea-a811-000d3aa4692b}.TM.blf
-rwxrwxrwx 1 root root 512K Dec  4 00:01  NTUSER.DAT{53b39e88-18c4-11ea-a811-000d3aa4692b}.TMContainer00000000000000000001.regtrans-ms
-rwxrwxrwx 1 root root 512K Dec  4 00:01  NTUSER.DAT{53b39e88-18c4-11ea-a811-000d3aa4692b}.TMContainer00000000000000000002.regtrans-ms
lrwxrwxrwx 1 root root   70 Dec  4 00:01  NetHood -> '/mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/Network Shortcuts'
drwxrwxrwx 1 root root  512 Dec  4 11:51  OneDrive
drwxrwxrwx 1 root root  512 Dec  4 00:05  Pictures
lrwxrwxrwx 1 root root   70 Dec  4 00:01  PrintHood -> '/mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/Printer Shortcuts'
lrwxrwxrwx 1 root root   59 Dec  4 00:01  Recent -> /mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/Recent
drwxrwxrwx 1 root root  512 Dec  4 00:03 'Saved Games'
drwxrwxrwx 1 root root  512 Dec  4 00:04  Searches
lrwxrwxrwx 1 root root   59 Dec  4 00:01  SendTo -> /mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/SendTo
drwxrwxrwx 1 root root  512 Dec  4 00:03  Videos
-rwxrwxrwx 1 root root 564K Dec  4 00:01  ntuser.dat.LOG1
-rwxrwxrwx 1 root root 548K Dec  4 00:01  ntuser.dat.LOG2
-rwxrwxrwx 1 root root   20 Dec  4 00:01  ntuser.ini
lrwxrwxrwx 1 root root   28 Dec  4 00:01 'Мои документы' -> /mnt/c/Users/serje/Documents
lrwxrwxrwx 1 root root   62 Dec  4 00:01  Шаблоны -> /mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/Templates
lrwxrwxrwx 1 root root   63 Dec  4 00:01 'главное меню' -> '/mnt/c/Users/serje/AppData/Roaming/Microsoft/Windows/Start Menu'
root@DESKTOP-LTI9L04:/mnt/c/Users/serje#
```
#### Создаем в Linux директорию для проекта и файлов конфигурации нового сервера:

```cmd
root@DESKTOP-LTI9L04:/mnt/c/Users/serje# mkdir -p Alfa && cd Alfa
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# pwd
/mnt/c/Users/serje/Alfa
```
