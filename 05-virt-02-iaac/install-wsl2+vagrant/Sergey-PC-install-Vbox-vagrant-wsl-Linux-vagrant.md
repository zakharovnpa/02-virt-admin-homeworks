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
```cmd
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# ls -lha
total 0
drwxrwxrwx 1 root root 512 Dec  4 18:29 .
drwxrwxrwx 1 root root 512 Dec  4 18:29 ..
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
```
#### При запуске Vagrant status не видит путь до файла CMD.exe
```yaml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant status
Vagrant failed to initialize at a very early stage:

The executable 'cmd.exe' Vagrant is trying to run was not
found in the PATH variable. This is an error. Please verify
this software is installed and on the path.
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
```
#### Смотрим переменные окружения
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# env
SHELL=/bin/bash
SUDO_GID=1000
SUDO_COMMAND=/bin/bash
SUDO_USER=maestro
PWD=/mnt/c/Users/serje/Alfa
LOGNAME=root
HOME=/root
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=root
SHLVL=1
XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
SUDO_UID=1000
MAIL=/var/mail/root
_=/usr/bin/env
OLDPWD=/mnt/c/Users/serje
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
```
#### Добавляем в файл ./bashrc поддержку WSL
```yml
 echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
```
#### Добавляем в файл ./bashrc пути и переменные окружения
##### Путь до исполняемого файла VirtualBox
```yml
echo 'export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc
```
##### Путь до системного каталога
```yml
echo 'export PATH="$PATH:/mnt/c/Windows/System32"' >> ~/.bashrc
```
##### Путь до исполняемого файла PowerShell
```yml
echo 'export PATH="$PATH:/mnt/c/Windows/System32/WindowsPowerShell/v1.0"' >> ~/.bashrc
```
#### Перезапускаем ./bashrc
```yml
source ~/.bashrc
```
#### Установка плагина поддержки WSL
```yml
vagrant plugin install virtualbox_WSL2
```
##### Результат
```cmd
Installing the 'virtualbox_WSL2' plugin. This can take a few minutes...
Fetching rake-13.0.6.gem
Fetching virtualbox_WSL2-0.1.3.gem
Installed the plugin 'virtualbox_WSL2 (0.1.3)'!
```
#### Проверяем статус  Vagrant
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant status
A Vagrant environment or target machine is required to run this
command. Run `vagrant init` to create a new Vagrant environment. Or,
get an ID of a target machine from `vagrant global-status` to run
this command on. A final option is to change to a directory with a
Vagrantfile and to try again.
```
```bash
Для выполнения этой команды требуется среда Vagrant или целевая машина. 
Запустите `vagrant init`, чтобы создать новую среду Vagrant. Или получите идентификатор целевой машины из vagrant global-status, 
чтобы запустить эту команду. Последний вариант - перейти в каталог с Vagrantfile и повторить попытку.
```
### Шаг 4. Инициализация Vagrant. Запуск тестовой ВМ для VirtualBox
#### Инициализируем Vagrant
##### В каталоге проекта Alfa выполняем инициализацию
```ps
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# ls -lha
total 0
drwxrwxrwx 1 root root 512 Dec  4 18:29 .
drwxrwxrwx 1 root root 512 Dec  4 19:15 ..
```
```yml
vagrant init
```
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```
```bash
В этот каталог помещен файл `Vagrantfile`. 
Теперь вы готовы «бродить» в своей первой виртуальной среде! 
Пожалуйста, прочтите комментарии в Vagrantfile, а также документацию 
на `vagrantup.com` для получения дополнительной информации об использовании Vagrant.
```
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# ls -lha
total 4.0K
drwxrwxrwx 1 root root  512 Dec  4 19:37 .
drwxrwxrwx 1 root root  512 Dec  4 19:15 ..
-rwxrwxrwx 1 root root 3.0K Dec  4 19:37 Vagrantfile
```

#### Содержимое файла Vagrantfile
```yaml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# cat Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
```
```cmd
Вся конфигурация Vagrant сделана ниже. «2» в Vagrant.configure настраивает версию конфигурации (мы поддерживаем старые стили для обратной совместимости). Пожалуйста, не меняйте его, если вы не знаете, что делаете.

Vagrant.configure ("2") do | config |

  Наиболее распространенные параметры конфигурации задокументированы и прокомментированы ниже. Полную справку см. В онлайн-документации по адресу https://docs.vagrantup.com.

Каждая среда разработки Vagrant требует коробки. Вы можете искать ящики на https://vagrantcloud.com/search.
 # config.vm.box = "base"

  Отключить автоматическую проверку обновлений ящика. Если вы отключите это, флажки будут проверяться на наличие обновлений только тогда, когда пользователь запускает `vagrant box outdated`. Это не рекомендуется.
  # config.vm.box_check_update = false

 Создайте переадресацию портов, которая разрешает доступ к определенному порту внутри машины с порта на хост-машине. В приведенном ниже примере при доступе к localhost: 8080 будет получен доступ к порту 80 на гостевой машине.
ПРИМЕЧАНИЕ: Это позволит общедоступному доступу к открытому порту.
  # config.vm.network "forwarded_port", гость: 80, хост: 8080

 Создайте перенаправленное сопоставление портов, которое разрешает доступ к определенному порту внутри машины с порта на хост-машине и разрешает доступ только через 127.0.0.1 для отключения общего доступа
  # config.vm.network "forwarded_port", гость: 80, хост: 8080, host_ip: "127.0.0.1"

 Создайте частную сеть, которая обеспечивает доступ к машине только для хоста с использованием определенного IP-адреса.
  # config.vm.network "private_network", ip: "192.168.33.10"

Создайте общедоступную сеть, которая обычно соответствует мостовой сети.
В мостовых сетях машина выглядит как другое физическое устройство в вашей сети.
  # config.vm.network "public_network"

 Поделитесь дополнительной папкой с гостевой виртуальной машиной. Первый аргумент - это путь на хосте к фактической папке. Второй аргумент - это гостевой путь для монтирования папки. И третий необязательный аргумент - это набор необязательных параметров.
  # config.vm.synced_folder "../data", "/ vagrant_data"

 Конфигурация для конкретного поставщика, чтобы вы могли точно настроить различных поставщиков поддержки для Vagrant. Они предоставляют параметры, зависящие от поставщика.
 Пример для VirtualBox:
  #
  # config.vm.provider "virtualbox" do | vb |
  # # Отображение графического интерфейса VirtualBox при загрузке машины
  # vb.gui = true
  #
Настройте объем памяти на виртуальной машине:
  # vb.memory = "1024"
  конец
  #
 См. Документацию к поставщику, которого вы используете, для получения дополнительных сведений о доступных параметрах.

Включите подготовку с помощью сценария оболочки. Также доступны дополнительные провайдеры, такие как Ansible, Chef, Docker, Puppet и Salt. См. Документацию для получения дополнительной информации об их синтаксисе и использовании.
  # config.vm.provision "shell", встроенный: << - SHELL
  # apt-get update
  # apt-get install -y apache2
  # ОБОЛОЧКА
конец
```

### Создаем свой файл Vagrantfile
```yaml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vim Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
        config.vm.box = "bento/ubuntu-20.04"
        config.ssh.host = 'localhost'
 end
```

```yaml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```
```cmd
Среда еще не создана. Запустите `vagrant up`, чтобы создать среду. 
Если машина не создана, будет показан только поставщик по умолчанию. 
Таким образом, если поставщика нет в списке, значит, машина не создана для этой среды.
```
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant ssh-config
The provider for this Vagrant-managed machine is reporting that it
is not yet ready for SSH. Depending on your provider this can carry
different meanings. Make sure your machine is created and running and
try again. Additionally, check the output of `vagrant status` to verify
that the machine is in the state that you expect. If you continue to
get this error message, please view the documentation for the provider
you're using.
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
```
```cmd
Поставщик этой машины под управлением Vagrant сообщает, что она еще не готова к SSH. 
В зависимости от вашего провайдера это может иметь разное значение. Убедитесь, что 
ваша машина создана и работает, и попробуйте еще раз. Кроме того, проверьте вывод 
«vagrant status», чтобы убедиться, что машина находится в ожидаемом состоянии. 
Если вы продолжаете получать это сообщение об ошибке, просмотрите документацию поставщика,
которого вы используете.
```
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant global-status
id       name   provider state  directory
--------------------------------------------------------------------
There are no active Vagrant environments on this computer! Or,
you haven't destroyed and recreated Vagrant environments that were
started with an older version of Vagrant.
```
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa# vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'bento/ubuntu-20.04' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'bento/ubuntu-20.04'
    default: URL: https://vagrantcloud.com/bento/ubuntu-20.04
==> default: Adding box 'bento/ubuntu-20.04' (v202107.28.0) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202107.28.0/providers/virtualbox.box
==> default: Successfully added box 'bento/ubuntu-20.04' (v202107.28.0) for 'virtualbox'!
==> default: Importing base box 'bento/ubuntu-20.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> default: Setting the name of the VM: Alfa_default_1638636885038_95987
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: localhost:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
    default: Warning: Connection refused. Retrying...
Timed out while waiting for the machine to boot. This means that
Vagrant was unable to communicate with the guest machine within
the configured ("config.vm.boot_timeout" value) time period.

If you look above, you should be able to see the error(s) that
Vagrant had when attempting to connect to the machine. These errors
are usually good hints as to what may be wrong.

If you're using a custom box, make sure that networking is properly
working and you're able to connect to the machine. It is a common
problem that networking isn't setup properly in these boxes.
Verify that authentication configurations are also setup properly,
as well.

If the box appears to be booting properly, you may want to increase
the timeout ("config.vm.boot_timeout") value.
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Alfa#
```
```bash
Истекло время ожидания загрузки машины. Это означает, что Vagrant не смог связаться с гостевой машиной 
в течение настроенного (значение "config.vm.boot_timeout") периода времени.

Если вы посмотрите выше, вы сможете увидеть ошибки, которые возникли у Vagrant при попытке подключиться 
к машине. Эти ошибки обычно служат хорошим намеком на то, что может быть не так.

Если вы используете настраиваемый ящик, убедитесь, что сеть работает правильно и вы можете подключиться 
к машине. Это обычная проблема, когда сеть не настроена должным образом в этих ящиках. 
Убедитесь, что конфигурации аутентификации также настроены правильно.

Если кажется, что ящик загружается правильно, вы можете увеличить значение тайм-аута 
("config.vm.boot_timeout").
```
### Шаг 5. Установка в WSL Ubuntu-20.04 ВМ проекта Betta
```yml
mkdir -p Betta && cd Betta
```
```yml
mkdir -p ansible && mkdir -p vagrant
```
#### Перейти в директорию ` vagrant ` и выполнить` vagrant status ` , ` vagrant init `
#### Конфигурационные файлы расположить в следующем порядке: 
##### В директории ` /Betta/vagrant ` файлы:
###### Заменить файл ` Vagrantfile ` на новое содержимое:
```yaml
# -*- mode: ruby -*-

ISO = "bento/ubuntu-20.04"
NET = "192.168.56."
DOMAIN = ".netology"
HOST_PREFIX = "server"
INVENTORY_PATH = "../ansible/inventory"

servers = [
  {
    :hostname => HOST_PREFIX + "1" + DOMAIN,
    :ip => NET + "11",
    :ssh_host => "20011",
    :ssh_vm => "22",
    :ram => 1024,
    :core => 1
  }
]

Vagrant.configure(2) do |config|
  config.vm.synced_folder ".", "/vagrant", disabled: false
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
    config.ssh.host = 'localhost'
      node.vm.box = ISO
      node.vm.hostname = machine[:hostname]
      node.vm.network "private_network", ip: machine[:ip]
      node.vm.network :forwarded_port, guest: machine[:ssh_vm], host: machine[:ssh_host]
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        vb.customize ["modifyvm", :id, "--cpus", machine[:core]]
        vb.name = machine[:hostname]
      end
      node.vm.provision "ansible" do |setup|
        setup.inventory_path = INVENTORY_PATH
        setup.playbook = "../ansible/provision.yml"
        setup.become = true
        setup.extra_vars = { ansible_user: 'vagrant' }
      end
    end
  end
end
```
###### ` ansible `
```yml
[defaults]
inventory=./inventory
deprecation_warnings=False
command_warnings=False
ansible_port=22
interpreter_python=/usr/bin/python3
```
##### В директории ` /Betta/ansible ` файлы:
###### ` inventory `
```yml
[nodes:children]
manager

[manager]
server1.netology ansible_host=127.0.0.1 ansible_port=20011 ansible_user=vagrant
```
###### ` provision.yaml `
```yml
---

  - hosts: nodes
    become: yes
    become_user: root
    remote_user: vagrant

    tasks:
      - name: Create directory for ssh-keys
        file: state=directory mode=0700 dest=/root/.ssh/

      - name: Adding rsa-key in /root/.ssh/authorized_keys
        copy: src=~/.ssh/id_rsa.pub dest=/root/.ssh/authorized_keys owner=root mode=0600
        ignore_errors: yes

      - name: Checking DNS
        command: host -t A google.com

      - name: Installing tools
        apt: >
          package={{ item }}
          state=present
          update_cache=yes
        with_items:
          - git
          - curl

      - name: Installing docker
        shell: curl -fsSL get.docker.com -o get-docker.sh && chmod +x get-docker.sh && ./get-docker.sh

      - name: Add the current user to docker group
        user: name=vagrant append=yes groups=docker
```
### Шаг 6. Запуск создание новой ВМ с помощью Vagrant && Ansible с автоматической установкой Docker
#### После неудачных попыток соединения по ssh из ОС Ubuntu WSL к новой ВМ, созданной Vagrant, было сделано следующее: WSL переведен на версию 1. Затем связь по  ssh появилась.
```yml
root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Betta/vagrant# vagrant provision
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...

PLAY [nodes] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [server1.netology]

TASK [Create directory for ssh-keys] *******************************************
changed: [server1.netology]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] ****************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: If you are using a module and expect the file to exist on the remote, see the remote_src option
fatal: [server1.netology]: FAILED! => {"changed": false, "msg": "Could not find or access '~/.ssh/id_rsa.pub' on the Ansible Controller.\nIf you are using a module and expect the file to exist on the remote, see the remote_src option"}
...ignoring

TASK [Checking DNS] ************************************************************
changed: [server1.netology]

TASK [Installing tools] ********************************************************
[DEPRECATION WARNING]: Invoking "apt" only once while using a loop via
squash_actions is deprecated. Instead of using a loop to supply multiple items
and specifying `package: "{{ item }}"`, please use `package: ['git', 'curl']`
and remove the loop. This feature will be removed in version 2.11. Deprecation
warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [server1.netology] => (item=['git', 'curl'])

TASK [Installing docker] *******************************************************
changed: [server1.netology]
[WARNING]: Consider using the get_url or uri module rather than running 'curl'.
If you need to use command because get_url or uri is insufficient you can add
'warn: false' to this command task or set 'command_warnings=False' in
ansible.cfg to get rid of this message.

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=1

root@DESKTOP-LTI9L04:/mnt/c/Users/serje/Betta/vagrant#
```
