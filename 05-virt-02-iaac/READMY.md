
# Домашнее задание к занятию "5.2. Применение принципов IaaC в работе с виртуальными машинами"

## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---

## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.
- Какой из принципов IaaC является основополагающим?

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

Задача:
* Установить на Windows 10 Домашняя систему виртуализации Virtualbox?
* Установить на Windows 10 Домашняя систему виртуализации WSL (Windows-Subsystem-Linux)
* Скачать и запустить в WSL дистрибутив Linux
* Установить в виртуальную ОС Linux систему управления виртуализацией vagrant
* Установить в виртуальную ОС Linux систему управления виртуализацией Virtualbox

Установка на Windows 10 Домашняя WSL 2: 
Из [статьи](https://www.thomasmaurer.ch/2019/06/install-wsl-2-on-windows-10/) команды выполненные в PowerShell под администратором:

```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
ПК перезагрузиться.

Затем выполнить:
```bash
Включить - WindowsOptionalFeature - Online - FeatureName VirtualMachinePlatform
```
ПК перезагрузиться.

Затем из [статьи](https://www.thomasmaurer.ch/2018/04/windows-subsystem-for-linux-on-windows-server/)
выполнить команды на  скачивание и установку дистрибутивов Linux

```bash
# For Ubuntu 16.04
 
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile ~/Ubuntu.zip -UseBasicParsing
 
# For Ubuntu 18.04
 
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1804 -OutFile ~/Ubuntu1804.zip -UseBasicParsing
 
# For OpenSUSE 42
 
Invoke-WebRequest -Uri https://aka.ms/wsl-opensuse-42 -OutFile ~/OpenSUSE.zip -UseBasicParsing
 
# For SLES 12
 
Invoke-WebRequest -Uri https://aka.ms/wsl-sles-12 -OutFile ~/SLES.zip -UseBasicParsing
```
Затем распаковать архив с дистрибутивом

```bash
Expand-Archive ~/Ubuntu.zip C:\Distros\Ubuntu
```
Затем запустить файл .exe. Установиться ВМ.

Установка WSL 2, Ubuntu, Vagrant по [статье How to run Vagrant + VirtualBox on WSL 2 (2021)](https://blog.thenets.org/how-to-run-vagrant-on-wsl-2/)

Команды:
```bash
# run inside WSL 2
# check https://www.vagrantup.com/downloads for more info
```

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

``bash
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

```bash
sudo apt-get update && sudo apt-get install vagrant
```

```bash
# append those two lines into ~/.bashrc
echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
echo 'export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc

# now reload the ~/.bashrc file
source ~/.bashrc
```

Лог установки:

```markdown
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)

PS C:\WINDOWS\system32> wsl -l -v
Нет установленных дистрибутивов подсистемы Windows для Linux.
Дистрибутивы можно установить из Microsoft Store:
https://aka.ms/wslstore

PS C:\WINDOWS\system32> wsl -l -o
-l: unrecognized option: o
(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Использование: wsl.exe [аргумент] [параметры...] [командная_строка]

Аргументы для запуска двоичного кода Linux:

    Если командная строка не указана, файл wsl.exe запускает стандартную оболочку.

    --exec, -e <командная_строка>
        Выполнение указанной команды без использования стандартной оболочки Linux.

    --
        Передача оставшейся командной строки как есть.

Параметры:
    --distribution, -d <распределение>
        Запуск указанного распределения.

    --user, -u <имя_пользователя>
        Запуск от имени указанного пользователя.

Аргументы для управления подсистемой Windows для Linux:

    --export <распределение> <имя_файла>
        Экспорт распределения в TAR-файл.
        В качестве имени стандартного выходного файла можно указать "-".

    --import <распределение> <расположение_установки> <имя_файла> [параметры]
        Импорт указанного TAR-файла в качестве нового распределения.
        В качестве имени стандартного выходного файла можно указать "-".

        Параметры:
            --version <версия>
                Specifies the version to use for the new distribution.

    --list, -l [параметры]
        Перечисление распределений.

        Параметры:
            --all
                Перечисляются все распределения, включая те, которые сейчас
                устанавливаются или удаляются.

            --running
                Перечисляются только те распределения, которые сейчас выполняются.

            --quiet, -q
                Отображаются только имена распределений.

            --verbose, -v
                Отображаются подробные сведения о всех распределениях.

    --set-default, -s <распределение>
        Распространение задается как стандартное.

    --set-default-version <версия>
        Изменение стандартной версии установки для новых распределений.

    --set-version <распределение> <версия>
        Изменение версии указанного распределения.

    --shutdown
        Все распределения, которые сейчас выполняются, немедленно прекращаются, и работа виртуальной машины средства облегченного доступа WSL 2 немедленно завершается.

    --terminate, -t <распределение>
        Указанное распределение прекращается.

    --unregister <распределение>
        Регистрация распространения отменяется.

    --help
        Отображение сведений об использовании.
PS C:\WINDOWS\system32>
PS C:\WINDOWS\system32> wsl -o -l
Недопустимый параметр в командной строке: -o
(c) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Использование: wsl.exe [аргумент] [параметры...] [командная_строка]

Аргументы для запуска двоичного кода Linux:

    Если командная строка не указана, файл wsl.exe запускает стандартную оболочку.

    --exec, -e <командная_строка>
        Выполнение указанной команды без использования стандартной оболочки Linux.

    --
        Передача оставшейся командной строки как есть.

Параметры:
    --distribution, -d <распределение>
        Запуск указанного распределения.

    --user, -u <имя_пользователя>
        Запуск от имени указанного пользователя.

Аргументы для управления подсистемой Windows для Linux:

    --export <распределение> <имя_файла>
        Экспорт распределения в TAR-файл.
        В качестве имени стандартного выходного файла можно указать "-".

    --import <распределение> <расположение_установки> <имя_файла> [параметры]
        Импорт указанного TAR-файла в качестве нового распределения.
        В качестве имени стандартного выходного файла можно указать "-".

        Параметры:
            --version <версия>
                Specifies the version to use for the new distribution.

    --list, -l [параметры]
        Перечисление распределений.

        Параметры:
            --all
                Перечисляются все распределения, включая те, которые сейчас
                устанавливаются или удаляются.

            --running
                Перечисляются только те распределения, которые сейчас выполняются.

            --quiet, -q
                Отображаются только имена распределений.

            --verbose, -v
                Отображаются подробные сведения о всех распределениях.

    --set-default, -s <распределение>
        Распространение задается как стандартное.

    --set-default-version <версия>
        Изменение стандартной версии установки для новых распределений.

    --set-version <распределение> <версия>
        Изменение версии указанного распределения.

    --shutdown
        Все распределения, которые сейчас выполняются, немедленно прекращаются, и работа виртуальной машины средства облегченного доступа WSL 2 немедленно завершается.

    --terminate, -t <распределение>
        Указанное распределение прекращается.

    --unregister <распределение>
        Регистрация распространения отменяется.

    --help
        Отображение сведений об использовании.
PS C:\WINDOWS\system32>
PS C:\WINDOWS\system32> wsl -l
Нет установленных дистрибутивов подсистемы Windows для Linux.
Дистрибутивы можно установить из Microsoft Store:
https://aka.ms/wslstore

PS C:\WINDOWS\system32> wsl -l -v
Нет установленных дистрибутивов подсистемы Windows для Linux.
Дистрибутивы можно установить из Microsoft Store:
https://aka.ms/wslstore

PS C:\WINDOWS\system32> nvoke-xpression "& { $(nvoke-estmethod https://aka.ms/install-powershell.ps1) } -se -review"
nvoke-estmethod : Имя "nvoke-estmethod" не распознано как имя командлета, функции, файла сценария или выполняемой прогр
аммы. Проверьте правильность написания имени, а также наличие и правильность пути, после чего повторите попытку.
строка:1 знак:24
+ nvoke-xpression "& { $(nvoke-estmethod https://aka.ms/install-powersh ...
+                        ~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (nvoke-estmethod:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

nvoke-xpression : Имя "nvoke-xpression" не распознано как имя командлета, функции, файла сценария или выполняемой прогр
аммы. Проверьте правильность написания имени, а также наличие и правильность пути, после чего повторите попытку.
строка:1 знак:1
+ nvoke-xpression "& { $(nvoke-estmethod https://aka.ms/install-powersh ...
+ ~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (nvoke-xpression:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\WINDOWS\system32> cd \
PS C:\> dir


    Каталог: C:\


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       21.01.2016     14:42                $WINDOWS.~Q
d-----       22.01.2020     18:09                AMD
d-----       14.01.2018     19:51                CheckPoint
d-----       16.11.2021     20:49                Distros
d-----       24.06.2016     20:42                DRIVERS
d-----       16.09.2021     22:13                ESD
d-----       25.10.2021     21:59                HashiCorp
d-----       14.05.2013      8:13                hp_LJ_M1120_Full_Solution
d-----       03.07.2019     19:49                inetpub
d-----       16.10.2020     13:27                Logs
d-----       14.05.2020     16:38                PerfLogs
d-r---       16.10.2021     20:41                Program Files
d-r---       21.08.2021     20:08                Program Files (x86)
d-----       04.08.2014     10:35                Programs
d-----       28.10.2021     10:43                tmp
d-r---       21.01.2020     21:55                Users
d-----       16.11.2021     20:11                Windows
d-----       03.07.2019     19:50                Windows10Upgrade
-a----       30.10.2015     19:41           1024 .rnd
-a----       21.11.2010      6:24        1828352 d3d9.dll
-a----       26.03.2017     13:43            235 JDiagnostics.ini
-a----       21.03.2005     14:49          25954 ListHardware.wsf
-ar---       21.03.2005     14:49          25903 ListSoftware.wsf
-a----       22.01.2016     13:16           8125 MyOutput-2.csv
-a----       22.01.2016     12:47          18572 MyOutput.csv
-a----       05.06.2003     22:13          53248 Process.exe


PS C:\>  cd C:\Distros\
PS C:\Distros> dir


    Каталог: C:\Distros


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       16.11.2021     20:49                Ubuntu


PS C:\Distros>
PS C:\Distros> cd .\Ubuntu\
PS C:\Distros\Ubuntu> dir


    Каталог: C:\Distros\Ubuntu


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       16.11.2021     20:49                AppxMetadata
d-----       16.11.2021     20:49                Assets
-a----       28.05.2019     15:35         197918 AppxBlockMap.xml
-a----       28.05.2019     15:35           3851 AppxManifest.xml
-a----       28.05.2019     15:36          11209 AppxSignature.p7x
-a----       28.05.2019     15:35      208117241 install.tar.gz
-a----       28.05.2019     15:35           5400 resources.pri
-a----       28.05.2019     15:35         211968 ubuntu1604.exe
-a----       28.05.2019     15:35            744 [Content_Types].xml


PS C:\Distros\Ubuntu> .\ubuntu1604.exe
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: maestro
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Installation successful!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

maestro@Sergey-PC:~$
maestro@Sergey-PC:~$ sudi -i
No command 'sudi' found, did you mean:
 Command 'sudo' from package 'sudo' (main)
 Command 'sudo' from package 'sudo-ldap' (universe)
sudi: command not found
maestro@Sergey-PC:~$ sudo -i
[sudo] password for maestro:
root@Sergey-PC:~#
root@Sergey-PC:~#
root@Sergey-PC:~# mc
The program 'mc' is currently not installed. You can install it by typing:
apt install mc
root@Sergey-PC:~# uname -a
Linux Sergey-PC 4.4.0-18362-Microsoft #1049-Microsoft Thu Aug 14 12:01:00 PST 2020 x86_64 x86_64 x86_64 GNU/Linux
root@Sergey-PC:~#
root@Sergey-PC:~#
root@Sergey-PC:~# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
root@Sergey-PC:~# sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
root@Sergey-PC:~#
root@Sergey-PC:~# sudo apt-get update && sudo apt-get install vagrant
Get:1 https://apt.releases.hashicorp.com xenial InRelease [8,654 B]
Get:2 https://apt.releases.hashicorp.com xenial/main amd64 Packages [35.9 kB]
Get:3 http://security.ubuntu.com/ubuntu xenial-security InRelease [109 kB]
Hit:4 http://archive.ubuntu.com/ubuntu xenial InRelease
Get:5 http://archive.ubuntu.com/ubuntu xenial-updates InRelease [109 kB]
Get:6 http://security.ubuntu.com/ubuntu xenial-security/main amd64 Packages [1,648 kB]
Get:7 http://archive.ubuntu.com/ubuntu xenial-backports InRelease [107 kB]
Get:8 http://archive.ubuntu.com/ubuntu xenial/universe amd64 Packages [7,532 kB]
Get:9 http://security.ubuntu.com/ubuntu xenial-security/main Translation-en [380 kB]
Get:10 http://security.ubuntu.com/ubuntu xenial-security/restricted amd64 Packages [9,824 B]
Get:11 http://security.ubuntu.com/ubuntu xenial-security/universe amd64 Packages [785 kB]
Get:12 http://security.ubuntu.com/ubuntu xenial-security/universe Translation-en [225 kB]
Get:13 http://security.ubuntu.com/ubuntu xenial-security/multiverse amd64 Packages [7,864 B]
Get:14 http://security.ubuntu.com/ubuntu xenial-security/multiverse Translation-en [2,672 B]
Get:15 http://archive.ubuntu.com/ubuntu xenial/universe Translation-en [4,354 kB]
Get:16 http://archive.ubuntu.com/ubuntu xenial/multiverse amd64 Packages [144 kB]
Get:17 http://archive.ubuntu.com/ubuntu xenial/multiverse Translation-en [106 kB]
Get:18 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [2,049 kB]
Get:19 http://archive.ubuntu.com/ubuntu xenial-updates/main Translation-en [482 kB]
Get:20 http://archive.ubuntu.com/ubuntu xenial-updates/restricted amd64 Packages [10.2 kB]
Get:21 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 Packages [1,219 kB]
Get:22 http://archive.ubuntu.com/ubuntu xenial-updates/universe Translation-en [358 kB]
Get:23 http://archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 Packages [22.6 kB]
Get:24 http://archive.ubuntu.com/ubuntu xenial-updates/multiverse Translation-en [8,476 B]
Get:25 http://archive.ubuntu.com/ubuntu xenial-backports/main amd64 Packages [9,812 B]
Get:26 http://archive.ubuntu.com/ubuntu xenial-backports/main Translation-en [4,456 B]
Get:27 http://archive.ubuntu.com/ubuntu xenial-backports/universe amd64 Packages [11.3 kB]
Get:28 http://archive.ubuntu.com/ubuntu xenial-backports/universe Translation-en [4,476 B]
Fetched 19.7 MB in 6min 48s (48.4 kB/s)
Reading package lists... Done
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no longer required:
  libfreetype6
Use 'sudo apt autoremove' to remove it.
The following NEW packages will be installed:
  vagrant
0 upgraded, 1 newly installed, 0 to remove and 163 not upgraded.
Need to get 41.5 MB of archives.
After this operation, 117 MB of additional disk space will be used.
Get:1 https://apt.releases.hashicorp.com xenial/main amd64 vagrant amd64 2.2.19 [41.5 MB]
Fetched 41.5 MB in 29s (1,402 kB/s)
Selecting previously unselected package vagrant.
(Reading database ... 25773 files and directories currently installed.)
Preparing to unpack .../vagrant_2.2.19_amd64.deb ...
Unpacking vagrant (2.2.19) ...
Setting up vagrant (2.2.19) ...
root@Sergey-PC:~#
root@Sergey-PC:~#
root@Sergey-PC:~#
```

Была ошибка при установке плагина:
```bash
root@Sergey-PC:~# vagrant plugin install virtualbox_WSL2
The executable 'cmd.exe' Vagrant is trying to run was not
found in the PATH variable. This is an error. Please verify
this software is installed and on the path.
root@Sergey-PC:~#
```
Решено прописыванием пути до файла CMD.exe
```bash
root@Sergey-PC:~# PATH=/mnt/c/Windows/System32:$PATH
root@Sergey-PC:~#
root@Sergey-PC:~# echo $PATH
/mnt/c/Windows/System32:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/mnt/c/Program Files/Oracle/VirtualBox
```
Успешная установка плагина:
```bash
root@Sergey-PC:~# vagrant plugin install virtualbox_WSL2
Installing the 'virtualbox_WSL2' plugin. This can take a few minutes...
Fetching rake-13.0.6.gem
Fetching virtualbox_WSL2-0.1.3.gem
Installed the plugin 'virtualbox_WSL2 (0.1.3)'!
root@Sergey-PC:~#
```

Теперь, когда у вас все установлено и настроено, давайте создадим простой проект hello world.

Вам нужно будет перейти к файлам Windows с помощью WSL, а затем запустить оттуда каждую команду Vagrant:

```bash
# Go to Windows user's dir from WSL
cd /mnt/c/Users/<my-user-name>/

# Create a project dir
mkdir -p projects/vagrant-demo
cd projects/vagrant-demo

# Create a Vagrantfile using Vagrant CLI
vagrant init hashicorp/bionic64
ls -l Vagrantfile

# Start a VM using Vagrantfile
vagrant up

# Login to the VM
# (password is 'vagrant')
vagrant ssh

# Done :)
```


При попытке запуска vagrant в ubuntu в wsl:

```bash
root@Sergey-PC:~#
root@Sergey-PC:~# type -a vagrant
root@Sergey-PC:~# n/vagrant
root@Sergey-PC:~#
root@Sergey-PC:~#
root@Sergey-PC:~#
root@Sergey-PC:~# mc
root@Sergey-PC:~#
root@Sergey-PC:~# clear
root@Sergey-PC:~#
root@Sergey-PC:~# cd /mnt/c/HashiCorp/Ubuntu-20.04-Vagrant/
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant#
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant# ls -lha
total 4.0K
drwxrwxrwx 1 root root  512 Nov 11 15:58 .
drwxrwxrwx 1 root root  512 Oct 25 21:59 ..
-rwxrwxrwx 1 root root    0 Nov 11 15:58 test-157.txt
drwxrwxrwx 1 root root  512 Sep 30 17:29 .vagrant
-rwxrwxrwx 1 root root 3.3K Oct 23 10:53 Vagrantfile
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant#
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant#
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant#
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant# ls -lha
total 4.0K
drwxrwxrwx 1 root root  512 Nov 11 15:58 .
drwxrwxrwx 1 root root  512 Oct 25 21:59 ..
-rwxrwxrwx 1 root root    0 Nov 11 15:58 test-157.txt
drwxrwxrwx 1 root root  512 Sep 30 17:29 .vagrant
-rwxrwxrwx 1 root root 3.3K Oct 23 10:53 Vagrantfile
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant#
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant# vagrant status
Vagrant failed to initialize at a very early stage:

Failed to locate the powershell executable on the available PATH. Please
ensure powershell is installed and available on the local PATH, then
run the command again.
root@Sergey-PC:/mnt/c/HashiCorp/Ubuntu-20.04-Vagrant# Работа экземпляра подсистемы Windows для Linux была завершена.
PS C:\Distros\Ubuntu>
PS C:\Distros\Ubuntu> wsl -l
Распределения подсистемы Windows для Linux:
Ubuntu-16.04 (по умолчанию)
PS C:\Distros\Ubuntu>
PS C:\Distros\Ubuntu>
PS C:\Distros\Ubuntu>


```

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

- Создать виртуальную машину.
- Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
```
docker ps
```
