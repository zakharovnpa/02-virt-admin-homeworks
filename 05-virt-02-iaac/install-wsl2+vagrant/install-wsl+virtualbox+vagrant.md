## Запуск ВМ в VirtualBox с помощью Vagrant в среде WSL (Windows-Subsystem-Linux)

Основная [статья](https://blog.thenets.org/how-to-run-vagrant-on-wsl-2/) с инструкцией

* Необходимо установить:
  - Windows 10 - версия +19042.928 (Версия 21H2)
  - VirtualBox - версия +6.1.30 (версия для Windows)
  - Vagrant - версия для Windows - должна совпадать с версией для Linux
  - WSL 2 - при необходимости. Можно оставить и WSL 1 (она установлена по умолчанию)
  - Vagrant +2.2.19 (версия для Linux)
  - Плагин Vagrant: virtualbox_WSL2


### Процедура запуска в WSL ОС Linux, установка и запуск в ней vagrant
#### Запускаем PowerShell:

```bash
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)
```
#### Проверяем конфигурацию системы
```bash
PS C:\WINDOWS\system32> systeminfo

Имя узла:                         DESKTOP-FMD4BBS
Название ОС:                      Майкрософт Windows 10 Домашняя
Версия ОС:                        10.0.19044 Н/Д построение 19044
Изготовитель ОС:                  Microsoft Corporation
Параметры ОС:                     Изолированная рабочая станция
Сборка ОС:                        Multiprocessor Free
Зарегистрированный владелец:      serjent@yandex.ru
Зарегистрированная организация:
Код продукта:                     00326-10000-00000-AA524
Дата установки:                   26.11.2021, 19:33:42
Время загрузки системы:           26.11.2021, 20:38:59
Изготовитель системы:             To Be Filled By O.E.M.
Модель системы:                   To Be Filled By O.E.M.
Тип системы:                      x64-based PC
Процессор(ы):                     Число процессоров - 1.
                                  [01]: AMD64 Family 16 Model 5 Stepping 3 AuthenticAMD ~3100 МГц
Версия BIOS:                      American Megatrends Inc. P1.40, 08.06.2011
Папка Windows:                    C:\WINDOWS
Системная папка:                  C:\WINDOWS\system32
Устройство загрузки:              \Device\HarddiskVolume1
Язык системы:                     ru;Русский
Язык ввода:                       ru;Русский
Часовой пояс:                     (UTC+04:00) Ижевск, Самара
Полный объем физической памяти:   7 932 МБ
Доступная физическая память:      4 324 МБ
Виртуальная память: Макс. размер: 10 236 МБ
Виртуальная память: Доступна:     5 180 МБ
Виртуальная память: Используется: 5 056 МБ
Расположение файла подкачки:      C:\pagefile.sys
Домен:                            WORKGROUP
Сервер входа в сеть:              \\DESKTOP-FMD4BBS
Исправление(я):                   Число установленных исправлений - 5.
                                  [01]: KB5004331
                                  [02]: KB5003791
                                  [03]: KB5007186
                                  [04]: KB5006753
                                  [05]: KB5005699
Сетевые адаптеры:                 Число сетевых адаптеров - 3.
                                  [01]: Qualcomm Atheros AR8151 PCI-E Gigabit Ethernet Controller (NDIS 6.30)
                                        Имя подключения: Ethernet
                                        DHCP включен:    Да
                                        DHCP-сервер:     192.168.1.1
                                        IP-адрес
                                        [01]: 192.168.1.25
                                        [02]: fe80::8987:d30f:c40e:d482
                                  [02]: ASUS PCE-N15 11n Wireless LAN PCI-E Card
                                        Имя подключения: Беспроводная сеть
                                        Состояние:       Носитель отключен
                                  [03]: VirtualBox Host-Only Ethernet Adapter
                                        Имя подключения: VirtualBox Host-Only Network
                                        DHCP включен:    Нет
                                        IP-адрес
                                        [01]: 192.168.56.1
                                        [02]: fe80::6194:2ab9:7e75:4eec
Требования Hyper-V:               Расширения режима мониторинга виртуальной машины: Да
                                  Виртуализация включена во встроенном ПО: Да
                                  Преобразование адресов второго уровня: Да
                                  Доступно предотвращение выполнения данных: Да
PS C:\WINDOWS\system32>
```

#### Запускаем WSL:
```bash
PS C:\WINDOWS\system32> wsl
```
#### Смотрим статус
```bash
PS C:\WINDOWS\system32> wsl --status
Распределение по умолчанию: Ubuntu-20.04
Версия по умолчанию: 2
Включите функцию Windows для платформы виртуальных машин и убедитесь в том, что в BIOS включена виртуализация.
Дополнительные сведения см. на странице https://aka.ms/wsl2-install
```



#### Смотрим установленные дистрибутивы:
```bash
PS C:\WINDOWS\system32> wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-20.04    Stopped         1
```
#### Смотрим доступные дистрибутивы:
```bash
PS C:\WINDOWS\system32> wsl -l -o
Ниже приведен список допустимых распределений, которые можно установить.
Установите с помощью команды wsl --install -d <Distro>.

NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
openSUSE-42     openSUSE Leap 42
SLES-12         SUSE Linux Enterprise Server v12
Ubuntu-16.04    Ubuntu 16.04 LTS
Ubuntu-18.04    Ubuntu 18.04 LTS
Ubuntu-20.04    Ubuntu 20.04 LTS
```
#### Запускаем Linux в WSL:
```bash
PS C:\WINDOWS\system32>
PS C:\WINDOWS\system32> wsl
maestro@DESKTOP-FMD4BBS:/mnt/c/WINDOWS/system32$
maestro@DESKTOP-FMD4BBS:/mnt/c/WINDOWS/system32$ uname -a
Linux DESKTOP-FMD4BBS 4.4.0-19041-Microsoft #1237-Microsoft Sat Sep 11 14:32:00 PST 2021 x86_64 x86_64 x86_64 GNU/Linux
maestro@DESKTOP-FMD4BBS:/mnt/c/WINDOWS/system32$
maestro@DESKTOP-FMD4BBS:/mnt/c/WINDOWS/system32$ sudo -i
[sudo] password for maestro:
root@DESKTOP-FMD4BBS:~#
```
#### Смотрим версию OC
```bash
root@DESKTOP-FMD4BBS:~# cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04 LTS"
NAME="Ubuntu"
VERSION="20.04 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

#### Создаем в Linux директорию для проекта и файлов конфигурации нового сервера:

```bash
root@DESKTOP-FMD4BBS:~#mkdir -p /Vagrant-project/server-1/
root@DESKTOP-FMD4BBS:~# cd /mnt/c/Users/serje/Vagrant-project/server-1/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```
#### Устанавливаем Vagrant внутри Linux на WSL по [мануалу](https://www.vagrantup.com/docs/other/wsl)
```bash
# run inside WSL 2
# check https://www.vagrantup.com/downloads for more info
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install vagrant
```
#### Смотрим версию vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2/ansible# vagrant --version
Vagrant 2.2.19
```
#### Запустили vagrant а он не находит путь до cmd.exe
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant status
Vagrant failed to initialize at a very early stage:

The executable 'cmd.exe' Vagrant is trying to run was not
found in the PATH variable. This is an error. Please verify
this software is installed and on the path.
```
#### Включаем поддержку WSL
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# echo 'export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```
#### Добавляем переменные окружения
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# echo 'export PATH="$PATH:/mnt/c/Windows/System32"' >> ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# echo 'export PATH="$PATH:/mnt/c/Windows/System32/WindowsPowerShell/1.0"' >> ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```
#### Перезапускаем ./bashrc
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# source ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```
#### Установка плагина поддержки WSL
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant plugin install virtualbox_WSL2
Installing the 'virtualbox_WSL2' plugin. This can take a few minutes...
Fetching rake-13.0.6.gem
Fetching virtualbox_WSL2-0.1.3.gem
Installed the plugin 'virtualbox_WSL2 (0.1.3)'!
```
#### Инициализируем vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant init
Vagrant failed to initialize at a very early stage:

Failed to locate the powershell executable on the available PATH. Please
ensure powershell is installed and available on the local PATH, then
run the command again.
```

Не найден путь к PowerShell. Ошибка в пути к файлу.

#### Проверяем переменные окружения:
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# env
SHELL=/bin/bash
SUDO_GID=1000
SUDO_COMMAND=/bin/bash
SUDO_USER=maestro
PWD=/mnt/c/Users/serje/Vagrant-project/server-1
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
VAGRANT_WSL_ENABLE_WINDOWS_ACCESS=1
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/mnt/c/Program Files/Oracle/VirtualBox:/mnt/c/Windows/System32:/mnt/c/Windows/System32/WindowsPowerShell/v1.0
SUDO_UID=1000
MAIL=/var/mail/root
OLDPWD=/root
_=/usr/bin/env
```
#### Корректируем путь до PowerShell
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# mc

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# echo 'export PATH="$PATH:/mnt/c/Windows/System32/WindowsPowerShell/v1.0"'
>> ~/.bashrc
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# mc

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.basic
  3. /usr/bin/mcedit
  4. /usr/bin/vim.tiny
  5. /bin/ed

Choose 1-5 [1]: 3
```

#### Перезапускаем ./bashrc
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# source ~/.bashrc
```
#### В каталоге проекта сервера инициализируем vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```
#### Смтрим появление файла конфигурации Vagrantfile
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# ls -lha
total 4.0K
drwxrwxrwx 1 maestro maestro 4.0K Nov 26 21:37 .
drwxrwxrwx 1 maestro maestro 4.0K Nov 26 20:52 ..
-rwxrwxrwx 1 maestro maestro 3.0K Nov 26 21:37 Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# mc
```
#### Корректируем файл Vagrantfile
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vim Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
        config.vm.box = "bento/ubuntu-20.04"
        config.ssh.host = 'localhost'
 end
```
#### Запускаем установку и запуск ОС Ubuntu-20.04
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant up
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
==> default: Setting the name of the VM: server-1_default_1637948535686_95805
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
    default: SSH address: 192.168.1.1:2222 # Здесь неверный адрес ВМ. Исправляется добавлением в Vagrantconfig параметра config.ssh.host = 'localhost'
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Attempting graceful shutdown of VM...

/opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:1214:in `__connect_nonblock': Operation already in progress - connect(2) for 192.168.1.1:2222 (Errno::EALREADY)
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```


#### Тем не менее ВМ создалась и запустилась.
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```
#### Останавливаем ВМ и добавляем параметр ` config.ssh.host = 'localhost' ` в Vagrantfile
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant halt
==> default: Attempting graceful shutdown of VM...
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1#
```

#### Запускаем ВМ с добавленным параметром ` config.ssh.host = 'localhost' ` в Vagrantfile
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> default: Clearing any previously set forwarded ports...
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
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /mnt/c/Users/serje/Vagrant-project/server-1
```
#### ВМ запущена. Подключаемся к ней по ssh.
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri 26 Nov 2021 05:58:05 PM UTC

  System load:  0.19              Processes:             118
  Usage of /:   2.3% of 61.31GB   Users logged in:       0
  Memory usage: 14%               IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
vagrant@vagrant:~$
vagrant@vagrant:~$
vagrant@vagrant:~$
```
#### Зашли в Ubuntu.
```bash
vagrant@vagrant:~$
vagrant@vagrant:~$ sudo -i
root@vagrant:~#
root@vagrant:~#
root@vagrant:~#
root@vagrant:~# mc
-bash: mc: command not found
root@vagrant:~#
root@vagrant:~#
root@vagrant:~#
root@vagrant:~#
root@vagrant:~# exit
logout
vagrant@vagrant:~$
vagrant@vagrant:~$
vagrant@vagrant:~$
vagrant@vagrant:~$ exit
logout
Connection to localhost closed.
```
#### Смотрим статус vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```
#### Остановка ВМ
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant halt
==> default: Attempting graceful shutdown of VM...
```
#### Смтрим статус
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-1# vagrant status
Current machine states:

default                   poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
```
