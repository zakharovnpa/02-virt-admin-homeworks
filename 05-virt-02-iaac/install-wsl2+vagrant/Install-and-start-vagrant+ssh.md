## На ПК Elena-PC запуск ВМ на WSL Ubuntu и запуск в ней ВМ с помощью Vagrant и  VirtualBox

### Входим в PowesrShell
```ps
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)

PS C:\Windows\system32>
PS C:\Windows\system32>
```
### Проверяем статус WSL
```ps
PS C:\Windows\system32> wsl --status
Распределение по умолчанию: Ubuntu-20.04
Версия по умолчанию: 2
Включите функцию Windows для платформы виртуальных машин и убедитесь в том, что в BIOS включена виртуализация.
Дополнительные сведения см. на странице https://aka.ms/wsl2-install
```
### Запускаем ВМ командой wsl. Можно ` wsl -d <Distrib> `
```ps
PS C:\Windows\system32> wsl
Welcome to Ubuntu 20.04 LTS (GNU/Linux 4.4.0-19041-Microsoft x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Dec  1 08:58:20 +04 2021

  System load:    0.52      Processes:             7
  Usage of /home: unknown   Users logged in:       0
  Memory usage:   60%       IPv4 address for eth0: 192.168.1.25
  Swap usage:     2%        IPv4 address for eth1: 192.168.56.1


271 updates can be installed immediately.
132 of these updates are security updates.
To see these additional updates run: apt list --upgradable

/usr/lib/ubuntu-release-upgrader/release-upgrade-motd: 31: cannot create /var/lib/ubuntu-release-upgrader/release-upgrade-available: Permission denied


This message is shown once once a day. To disable it please create the
/home/maestro/.hushlogin file.
```
  ### Входим в УЗ администратора  
```ps
maestro@DESKTOP-FMD4BBS:/mnt/c/Windows/system32$ sudo -i
[sudo] password for maestro:
Welcome to Ubuntu 20.04 LTS (GNU/Linux 4.4.0-19041-Microsoft x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Dec  1 08:59:07 +04 2021

  System load:    0.52      Processes:             9
  Usage of /home: unknown   Users logged in:       0
  Memory usage:   60%       IPv4 address for eth0: 192.168.1.25
  Swap usage:     2%        IPv4 address for eth1: 192.168.56.1


271 updates can be installed immediately.
132 of these updates are security updates.
To see these additional updates run: apt list --upgradable



This message is shown once once a day. To disable it please create the
/root/.hushlogin file.
root@DESKTOP-FMD4BBS:~#
```
### Смотрим что Vagrant уже бфл установлен
```ps
root@DESKTOP-FMD4BBS:~# type vagrant
vagrant is /usr/bin/vagrant
```
### Команды для установки Vagrant
#### Скачивание и установка ключа для подключения к репозиторию Hashicorp
```ps
root@DESKTOP-FMD4BBS:~# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
```
#### Подключение репозитория Hashicorp
```ps
root@DESKTOP-FMD4BBS:~#
root@DESKTOP-FMD4BBS:~# apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Hit:4 https://apt.releases.hashicorp.com focal InRelease
Get:5 http://archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1387 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [281 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [14.6 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [606 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [86.8 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 c-n-f Metadata [528 B]
Get:12 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [877 kB]
Get:13 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1062 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [190 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [19.6 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [41.2 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [9732 B]
Get:18 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [516 B]
Get:19 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [18.9 kB]
Get:20 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [7524 B]
Get:21 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [644 B]
Get:22 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [196 kB]
Get:23 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [9076 B]
Get:24 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [560 kB]
Get:25 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [80.2 kB]
Get:26 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 c-n-f Metadata [528 B]
Fetched 5784 kB in 12s (481 kB/s)
Reading package lists... Done
```
#### Обновляем установщики
```ps
root@DESKTOP-FMD4BBS:~# apt-get update
Hit:1 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu focal InRelease
Hit:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:5 https://apt.releases.hashicorp.com focal InRelease
Reading package lists... Done
```
#### Установка Vagrant
```ps
root@DESKTOP-FMD4BBS:~# apt-get install vagrant
Reading package lists... Done
Building dependency tree
Reading state information... Done
vagrant is already the newest version (2.2.19).
0 upgraded, 0 newly installed, 0 to remove and 251 not upgraded.
```
### Создаем новую директорию проекта Alfa.
```ps

root@DESKTOP-FMD4BBS:~# cd /mnt/c/Users/serje/Vagrant-project/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project# mkdir -p Alfa
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project# cd Alfa/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# ls -lha
total 0
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:32 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:31 ..
```
### Проверяем статус Vagrant
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant status
A Vagrant environment or target machine is required to run this
command. Run `vagrant init` to create a new Vagrant environment. Or,
get an ID of a target machine from `vagrant global-status` to run
this command on. A final option is to change to a directory with a
Vagrantfile and to try again.
```
### Инициализируем в папке проекта конфигурацию для запуска новой ВМ
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```
### В результате создан дефолтный Vagrantfile
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# ls -lha
total 4.0K
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:33 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:31 ..
-rwxrwxrwx 1 maestro maestro 3.0K Dec  1 09:33 Vagrantfile
```
### Корректируем Vagrantfile
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
```
###
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# env
SHELL=/bin/bash
SUDO_GID=1000
SUDO_COMMAND=/bin/bash
SUDO_USER=maestro
PWD=/mnt/c/Users/serje/Vagrant-project/Alfa
LOGNAME=root
MOTD_SHOWN=update-motd
HOME=/root
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
VAGRANT_DEFAULT_PROVIDER=virtualbox
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
_=/usr/bin/env
OLDPWD=/mnt/c/Users/serje/Vagrant-project
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant --version
Vagrant 2.2.19
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant up
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
==> default: Setting the name of the VM: Alfa_default_1638337834012_66150
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
    default: SSH address: 192.168.1.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Attempting graceful shutdown of VM...
==> default: Attempting graceful shutdown of VM...
==> default: Attempting graceful shutdown of VM...
^C==> default: Waiting for cleanup before exiting...
Vagrant exited after cleanup due to external interrupt.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant ssh
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant halt
==> default: Attempting graceful shutdown of VM...
Traceback (most recent call last):
        70: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/bin/vagrant:231:in `<main>'
        69: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/environment.rb:290:in `cli'
        68: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/cli.rb:67:in `execute'
        67: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/commands/halt/command.rb:30:in `execute'
        66: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/plugin/v2/command.rb:232:in `with_target_vms'
        65: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/plugin/v2/command.rb:232:in `each'
        64: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/plugin/v2/command.rb:243:in `block in with_target_vms'
        63: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/commands/halt/command.rb:31:in `block in execute'
        62: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/machine.rb:201:in `action'
        61: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/machine.rb:201:in `call'
        60: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/environment.rb:614:in `lock'
        59: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/machine.rb:215:in `block in action'
        58: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/machine.rb:246:in `action_raw'
        57: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `run'
        56: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/util/busy.rb:19:in `busy'
        55: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `block in run'
        54: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builder.rb:149:in `call'
        53: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        52: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/providers/virtualbox/action/check_virtualbox.rb:26:in `call'
        51: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        50: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builtin/call.rb:53:in `call'
        49: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `run'
        48: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/util/busy.rb:19:in `busy'
        47: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `block in run'
        46: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builder.rb:149:in `call'
        45: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        44: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:127:in `block in finalize_action'
        43: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        42: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/providers/virtualbox/action/check_accessible.rb:18:in `call'
        41: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        40: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/providers/virtualbox/action/discard_state.rb:15:in `call'
        39: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        38: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builtin/call.rb:53:in `call'
        37: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `run'
        36: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/util/busy.rb:19:in `busy'
        35: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `block in run'
        34: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builder.rb:149:in `call'
        33: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        32: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:127:in `block in finalize_action'
        31: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        30: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:127:in `block in finalize_action'
        29: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        28: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builtin/call.rb:43:in `call'
        27: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `run'
        26: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/util/busy.rb:19:in `busy'
        25: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/runner.rb:89:in `block in run'
        24: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builder.rb:149:in `call'
        23: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/warden.rb:48:in `call'
        22: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/action/builtin/graceful_halt.rb:50:in `call'
        21: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/machine.rb:281:in `guest'
        20: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/communicators/ssh/communicator.rb:149:in `ready?'
        19: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/communicators/ssh/communicator.rb:432:in `connect'
        18: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/lib/vagrant/util/retryable.rb:17:in `retryable'
        17: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/communicators/ssh/communicator.rb:433:in `block in connect'
        16: from /opt/vagrant/embedded/lib/ruby/2.7.0/timeout.rb:110:in `timeout'
        15: from /opt/vagrant/embedded/lib/ruby/2.7.0/timeout.rb:33:in `catch'
        14: from /opt/vagrant/embedded/lib/ruby/2.7.0/timeout.rb:33:in `catch'
        13: from /opt/vagrant/embedded/lib/ruby/2.7.0/timeout.rb:33:in `block in catch'
        12: from /opt/vagrant/embedded/lib/ruby/2.7.0/timeout.rb:95:in `block in timeout'
        11: from /opt/vagrant/embedded/gems/2.2.19/gems/vagrant-2.2.19/plugins/communicators/ssh/communicator.rb:467:in `block (2 levels) in connect'
        10: from /opt/vagrant/embedded/gems/2.2.19/gems/net-ssh-6.1.0/lib/net/ssh.rb:251:in `start'
         9: from /opt/vagrant/embedded/gems/2.2.19/gems/net-ssh-6.1.0/lib/net/ssh.rb:251:in `new'
         8: from /opt/vagrant/embedded/gems/2.2.19/gems/net-ssh-6.1.0/lib/net/ssh/transport/session.rb:73:in `initialize'
         7: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:632:in `tcp'
         6: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:227:in `foreach'
         5: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:227:in `each'
         4: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:642:in `block in tcp'
         3: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:137:in `connect'
         2: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:56:in `connect_internal'
         1: from /opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:1214:in `connect_nonblock'
/opt/vagrant/embedded/lib/ruby/2.7.0/socket.rb:1214:in `__connect_nonblock': Operation already in progress - connect(2) for 192.168.1.1:2222 (Errno::EALREADY)
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant ssh-config
Host default
  HostName 192.168.1.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /mnt/c/Users/serje/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant ssh-config
Host default
  HostName localhost
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /mnt/c/Users/serje/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant halt
==> default: Attempting graceful shutdown of VM...
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant status
Current machine states:

default                   poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant up
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
    default: /vagrant => /mnt/c/Users/serje/Vagrant-project/Alfa
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed 01 Dec 2021 06:02:05 AM UTC

  System load:  0.34              Processes:             111
  Usage of /:   2.3% of 61.31GB   Users logged in:       0
  Memory usage: 14%               IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
vagrant@vagrant:~$
vagrant@vagrant:~$
vagrant@vagrant:~$ exit
logout
Connection to localhost closed.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
```
