## Шаг 1. процесса установки на ПК Sergey-PC Virtualbox, Vagrant, запуска WSL и одновременно с ней запуск компонента ОС Linux.

### . 
```yml
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)

PS C:\Windows\system32>
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
### Малый вариант вывода команды ` wsl -l -v `
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
