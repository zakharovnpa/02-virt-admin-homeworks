## Установка на PC-Sergey на реальной ОС Ubuntu VirtualBox
### 
```yml
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

maestro@PC-Ubuntu:~/Рабочий стол$ sudo -i
[sudo] пароль для maestro: 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# cd etc/apt/
-bash: cd: etc/apt/: Нет такого файла или каталога
root@PC-Ubuntu:~# cd /etc/apt/
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# ls -l
итого 24
drwxr-xr-x 2 root root 4096 дек  5 13:11 apt.conf.d
drwxr-xr-x 2 root root 4096 апр  9  2020 auth.conf.d
drwxr-xr-x 2 root root 4096 апр  9  2020 preferences.d
-rw-rw-r-- 1 root root 3158 дек  5 13:11 sources.list
drwxr-xr-x 2 root root 4096 апр  9  2020 sources.list.d
drwxr-xr-x 2 root root 4096 авг 19 14:30 trusted.gpg.d
root@PC-Ubuntu:/etc/apt# cat apt.conf.d/
cat: apt.conf.d/: Это каталог
root@PC-Ubuntu:/etc/apt# cd apt.conf.d/
root@PC-Ubuntu:/etc/apt/apt.conf.d# 
```
```yml
root@PC-Ubuntu:/etc/apt/apt.conf.d# ls -l
итого 84
-rw-rw-r-- 1 root root   49 дек  5 13:07 00aptitude
-rw-rw-r-- 1 root root   40 дек  5 13:06 00trustcdrom
-rw-r--r-- 1 root root  630 апр  9  2020 01autoremove
-r--r--r-- 1 root root 1455 дек  5 13:11 01autoremove-kernels
-rw-r--r-- 1 root root   92 апр  9  2020 01-vendor-ubuntu
-rw-r--r-- 1 root root  129 мая 14  2021 10periodic
-rw-r--r-- 1 root root  108 мая 14  2021 15update-stamp
-rw-r--r-- 1 root root  604 июл 27 17:54 20apt-esm-hook.conf
-rw-r--r-- 1 root root   85 мая 14  2021 20archive
-rw-r--r-- 1 root root   80 июл 21  2020 20auto-upgrades
-rw-r--r-- 1 root root  243 дек 16  2009 20dbus
-rw-r--r-- 1 root root 1040 сен 23  2020 20packagekit
-rw-r--r-- 1 root root  114 мар 26  2021 20snapd.conf
-rw-r--r-- 1 root root 2592 янв 18  2020 50appstream
-rw-r--r-- 1 root root  625 окт  7  2019 50command-not-found
-rw-r--r-- 1 root root 5459 июл 21  2020 50unattended-upgrades
-rw-r--r-- 1 root root  435 янв 18  2020 60icons
-rw-r--r-- 1 root root  251 янв 18  2020 60icons-hidpi
-rw-r--r-- 1 root root  182 авг  3  2019 70debconf
-rw-r--r-- 1 root root  305 мая 14  2021 99update-notifier
root@PC-Ubuntu:/etc/apt/apt.conf.d# cd ..
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# ls -l
итого 24
drwxr-xr-x 2 root root 4096 дек  5 13:11 apt.conf.d
drwxr-xr-x 2 root root 4096 апр  9  2020 auth.conf.d
drwxr-xr-x 2 root root 4096 апр  9  2020 preferences.d
-rw-rw-r-- 1 root root 3158 дек  5 13:11 sources.list
drwxr-xr-x 2 root root 4096 апр  9  2020 sources.list.d
drwxr-xr-x 2 root root 4096 авг 19 14:30 trusted.gpg.d
```
```yml
root@PC-Ubuntu:/etc/apt# cat sources.list
#deb cdrom:[Ubuntu 20.04.3 LTS _Focal Fossa_ - Release amd64 (20210819)]/ focal main restricted

# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://ru.archive.ubuntu.com/ubuntu/ focal main restricted
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://ru.archive.ubuntu.com/ubuntu/ focal-updates main restricted
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://ru.archive.ubuntu.com/ubuntu/ focal universe
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal universe
deb http://ru.archive.ubuntu.com/ubuntu/ focal-updates universe
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu 
## team, and may not be under a free licence. Please satisfy yourself as to 
## your rights to use the software. Also, please note that software in 
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://ru.archive.ubuntu.com/ubuntu/ focal multiverse
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal multiverse
deb http://ru.archive.ubuntu.com/ubuntu/ focal-updates multiverse
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal-updates multiverse

## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
deb http://ru.archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
# deb-src http://ru.archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse

## Uncomment the following two lines to add software from Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu focal partner
# deb-src http://archive.canonical.com/ubuntu focal partner

deb http://security.ubuntu.com/ubuntu focal-security main restricted
# deb-src http://security.ubuntu.com/ubuntu focal-security main restricted
deb http://security.ubuntu.com/ubuntu focal-security universe
# deb-src http://security.ubuntu.com/ubuntu focal-security universe
deb http://security.ubuntu.com/ubuntu focal-security multiverse
# deb-src http://security.ubuntu.com/ubuntu focal-security multiverse

# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
root@PC-Ubuntu:/etc/apt# cat sources.list | less
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# vim sources.list

Команда «vim» не найдена, но может быть установлена с помощью:

apt install vim         # version 2:8.1.2269-1ubuntu5.4, or
apt install vim-tiny    # version 2:8.1.2269-1ubuntu5.4
apt install vim-athena  # version 2:8.1.2269-1ubuntu5.4
apt install vim-gtk3    # version 2:8.1.2269-1ubuntu5.4
apt install vim-nox     # version 2:8.1.2269-1ubuntu5.4
apt install neovim      # version 0.4.3-3
```
```yml
root@PC-Ubuntu:/etc/apt# apt install vim
Ожидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/locОжидание блокировки кэша: Не удалось по^Cидание блокировки кэша: Не удалось получить блокировку файла /var/lib/dpkg/lock-frontend. Она удерживается процессом 5230 (aptd)… 153се удалось получить блокировку файла /var/lib/dpkg/lock-frontend. Онroot@PC-Ubuntu:/etc/apt# 5230 (aptd)… 138сь блокировку файла /var/lib/dpkg/lock-frontend. Она удерживается процессом 5230 (aptd)… 137с
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# apt install vim
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  vim-runtime
Предлагаемые пакеты:
  ctags vim-doc vim-scripts
Следующие НОВЫЕ пакеты будут установлены:
  vim vim-runtime
Обновлено 0 пакетов, установлено 2 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 7 114 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 34,6 MB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 vim-runtime all 2:8.1.2269-1ubuntu5.4 [5 875 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 vim amd64 2:8.1.2269-1ubuntu5.4 [1 239 kB]
Получено 7 114 kB за 2с (3 224 kB/s)
Выбор ранее не выбранного пакета vim-runtime.
(Чтение базы данных … на данный момент установлено 188334 файла и каталога.)
Подготовка к распаковке …/vim-runtime_2%3a8.1.2269-1ubuntu5.4_all.deb …
Добавляется «отклонение /usr/share/vim/vim81/doc/help.txt в /usr/share/vim/vim81/doc/help.txt.vim-tiny из-за vim-runtime»
Добавляется «отклонение /usr/share/vim/vim81/doc/tags в /usr/share/vim/vim81/doc/tags.vim-tiny из-за vim-runtime»
Распаковывается vim-runtime (2:8.1.2269-1ubuntu5.4) …
Выбор ранее не выбранного пакета vim.
Подготовка к распаковке …/vim_2%3a8.1.2269-1ubuntu5.4_amd64.deb …
Распаковывается vim (2:8.1.2269-1ubuntu5.4) …
Настраивается пакет vim-runtime (2:8.1.2269-1ubuntu5.4) …
Настраивается пакет vim (2:8.1.2269-1ubuntu5.4) …
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/vim (vim) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/vimdiff (vimdiff) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/rvim (rvim) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/rview (rview) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/vi (vi) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/view (view) в автоматическом режиме
update-alternatives: используется /usr/bin/vim.basic для предоставления /usr/bin/ex (ex) в автоматическом режиме
Обрабатываются триггеры для man-db (2.9.1-1) …
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# vim sources.list
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# apt-key add oracle_vbox_2016.asc
gpg: не могу открыть 'oracle_vbox_2016.asc': Нет такого файла или каталога
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
OK
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
OK
```
```yml
root@PC-Ubuntu:/etc/apt# apt-get update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                         
Пол:4 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                   
Пол:5 https://download.virtualbox.org/virtualbox/debian bionic InRelease [4 432 B]                   
Пол:6 http://security.ubuntu.com/ubuntu focal-security/main amd64 DEP-11 Metadata [35,7 kB]
Пол:7 http://security.ubuntu.com/ubuntu focal-security/universe amd64 DEP-11 Metadata [64,5 kB]
Пол:8 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 DEP-11 Metadata [2 464 B]
Пол:9 https://download.virtualbox.org/virtualbox/debian bionic/contrib amd64 Packages [1 908 B]
Получено 223 kB за 2с (98,1 kB/s)          
Чтение списков пакетов… Готово
```
```yml
root@PC-Ubuntu:/etc/apt# apt-get install virtualbox-6.1
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Некоторые пакеты не могут быть установлены. Возможно, то, что вы просите,
неосуществимо, или же вы используете нестабильную версию дистрибутива, где
запрошенные вами пакеты ещё не созданы или были удалены из Incoming.
Следующая информация, возможно, вам поможет:

Следующие пакеты имеют неудовлетворённые зависимости:
 virtualbox-6.1 : Зависит: libvpx5 (>= 1.6.0) но он не может быть установлен
                  Рекомендует: libsdl-ttf2.0-0 но он не будет установлен
                  Рекомендует: gcc но он не будет установлен
                  Рекомендует: make или
                                          build-essential но он не будет установлен или
                                          dpkg-dev но он не будет установлен
                  Рекомендует: binutils но он не будет установлен
E: Невозможно исправить ошибки: у вас зафиксированы сломанные пакеты.
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# apt-get install libvpx5
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Пакет libvpx5 недоступен, но упомянут в списке зависимостей другого
пакета. Это может означать, что пакет отсутствует, устарел или
доступен из источников, не упомянутых в sources.list

E: Для пакета «libvpx5» не найден кандидат на установку
root@PC-Ubuntu:/etc/apt# 
```
```yml
root@PC-Ubuntu:/etc/apt# sudo apt update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease                                                                
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                                                              
Сущ:4 http://security.ubuntu.com/ubuntu focal-security InRelease                                                               
Сущ:5 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                       
Чтение списков пакетов… Готово            
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Может быть обновлено 3 пакета. Запустите «apt list --upgradable» для их показа.
```
```yml
root@PC-Ubuntu:/etc/apt# sudo apt-get install virtualbox-6.1
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Некоторые пакеты не могут быть установлены. Возможно, то, что вы просите,
неосуществимо, или же вы используете нестабильную версию дистрибутива, где
запрошенные вами пакеты ещё не созданы или были удалены из Incoming.
Следующая информация, возможно, вам поможет:

Следующие пакеты имеют неудовлетворённые зависимости:
 virtualbox-6.1 : Зависит: libvpx5 (>= 1.6.0) но он не может быть установлен
                  Рекомендует: libsdl-ttf2.0-0 но он не будет установлен
                  Рекомендует: gcc но он не будет установлен
                  Рекомендует: make или
                                          build-essential но он не будет установлен или
                                          dpkg-dev но он не будет установлен
                  Рекомендует: binutils но он не будет установлен
E: Невозможно исправить ошибки: у вас зафиксированы сломанные пакеты.
```
```yml
root@PC-Ubuntu:/etc/apt# Email

Команда «Email» не найдена. Возможно, вы имели в виду:

  command 'mail' from deb mailutils (1:3.7-2.1)
  command 'wmail' from deb wmail (2.3-1)
  command 'dmail' from deb uw-mailutils (8:2007f~dfsg-7)
  command 'tmail' from deb uw-mailutils (8:2007f~dfsg-7)
  command 'cmail' from deb xboard (4.9.1-1build1)
  command 'kmail' from deb kmail (4:19.12.3-0ubuntu1)
  command 'rmail' from deb exim4-daemon-heavy (4.93-13ubuntu1.5)
  command 'rmail' from deb exim4-daemon-light (4.93-13ubuntu1.5)
  command 'rmail' from deb postfix (3.4.13-0ubuntu1.2)
  command 'rmail' from deb courier-mta (1.0.6-1build2)
  command 'rmail' from deb masqmail (0.3.4-1build1)
  command 'rmail' from deb rmail (8.15.2-18)
```
```yml
root@PC-Ubuntu:/etc/apt# add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib"
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease                                                              
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                                                                                                                              
Сущ:4 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                                                                         
Пол:5 http://download.virtualbox.org/virtualbox/debian focal InRelease [4 428 B]                                                                                         
Сущ:6 http://security.ubuntu.com/ubuntu focal-security InRelease                  
Пол:7 http://download.virtualbox.org/virtualbox/debian focal/contrib amd64 Packages [1 504 B]
Получено 5 932 B за 1с (4 331 B/s)      
Чтение списков пакетов… Готово
```
```yml
root@PC-Ubuntu:/etc/apt# apt-get install virtualbox-6.1
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  binutils binutils-common binutils-x86-64-linux-gnu gcc gcc-9 libasan5 libatomic1 libbinutils libc-dev-bin libc6-dev libcrypt-dev libctf-nobfd0 libctf0 libdouble-conversion3 libgcc-9-dev libitm1
  liblsan0 libpcre2-16-0 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5opengl5 libqt5printsupport5 libqt5svg5 libqt5widgets5 libqt5x11extras5 libquadmath0 libsdl-ttf2.0-0 libsdl1.2debian
  libtsan0 libubsan1 libxcb-xinerama0 libxcb-xinput0 linux-libc-dev make manpages-dev qt5-gtk-platformtheme qttranslations5-l10n
Предлагаемые пакеты:
  binutils-doc gcc-multilib autoconf automake libtool flex bison gcc-doc gcc-9-multilib gcc-9-doc gcc-9-locales glibc-doc qt5-image-formats-plugins qtwayland5 make-doc
Следующие НОВЫЕ пакеты будут установлены:
  binutils binutils-common binutils-x86-64-linux-gnu gcc gcc-9 libasan5 libatomic1 libbinutils libc-dev-bin libc6-dev libcrypt-dev libctf-nobfd0 libctf0 libdouble-conversion3 libgcc-9-dev libitm1
  liblsan0 libpcre2-16-0 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5opengl5 libqt5printsupport5 libqt5svg5 libqt5widgets5 libqt5x11extras5 libquadmath0 libsdl-ttf2.0-0 libsdl1.2debian
  libtsan0 libubsan1 libxcb-xinerama0 libxcb-xinput0 linux-libc-dev make manpages-dev qt5-gtk-platformtheme qttranslations5-l10n virtualbox-6.1
Обновлено 0 пакетов, установлено 40 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 128 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 374 MB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libdouble-conversion3 amd64 3.1.5-4ubuntu1 [37,9 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libpcre2-16-0 amd64 10.34-7 [181 kB]                     
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5core5a amd64 5.12.8+dfsg-0ubuntu1 [2 005 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5dbus5 amd64 5.12.8+dfsg-0ubuntu1 [208 kB]
Пол:5 http://download.virtualbox.org/virtualbox/debian focal/contrib amd64 virtualbox-6.1 amd64 6.1.30-148432~Ubuntu~eoan [93,4 MB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5network5 amd64 5.12.8+dfsg-0ubuntu1 [674 kB]
Пол:7 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libxcb-xinerama0 amd64 1.14-2 [5 260 B]
Пол:8 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libxcb-xinput0 amd64 1.14-2 [29,3 kB]
Пол:9 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5gui5 amd64 5.12.8+dfsg-0ubuntu1 [2 971 kB]
Пол:10 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5widgets5 amd64 5.12.8+dfsg-0ubuntu1 [2 293 kB]
Пол:11 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5svg5 amd64 5.12.8-0ubuntu1 [131 kB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5opengl5 amd64 5.12.8+dfsg-0ubuntu1 [136 kB]
Пол:13 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5printsupport5 amd64 5.12.8+dfsg-0ubuntu1 [193 kB]
Пол:14 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libqt5x11extras5 amd64 5.12.8-0ubuntu1 [10,3 kB]
Пол:15 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libsdl1.2debian amd64 1.2.15+dfsg2-5 [175 kB]
Пол:16 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-common amd64 2.34-6ubuntu1.3 [207 kB]
Пол:17 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libbinutils amd64 2.34-6ubuntu1.3 [474 kB]
Пол:18 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf-nobfd0 amd64 2.34-6ubuntu1.3 [47,4 kB]
Пол:19 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libctf0 amd64 2.34-6ubuntu1.3 [46,6 kB]
Пол:20 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils-x86-64-linux-gnu amd64 2.34-6ubuntu1.3 [1 613 kB]
Пол:21 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 binutils amd64 2.34-6ubuntu1.3 [3 380 B]
Пол:22 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libitm1 amd64 10.3.0-1ubuntu1~20.04 [26,2 kB]
Пол:23 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libatomic1 amd64 10.3.0-1ubuntu1~20.04 [9 284 B]
Пол:24 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libasan5 amd64 9.3.0-17ubuntu1~20.04 [394 kB]
Пол:25 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 liblsan0 amd64 10.3.0-1ubuntu1~20.04 [835 kB]
Пол:26 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libtsan0 amd64 10.3.0-1ubuntu1~20.04 [2 009 kB]
Пол:27 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libubsan1 amd64 10.3.0-1ubuntu1~20.04 [784 kB]
Пол:28 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libquadmath0 amd64 10.3.0-1ubuntu1~20.04 [146 kB]
Пол:29 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libgcc-9-dev amd64 9.3.0-17ubuntu1~20.04 [2 360 kB]
Пол:30 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 gcc-9 amd64 9.3.0-17ubuntu1~20.04 [8 241 kB]
Пол:31 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 gcc amd64 4:9.3.0-1ubuntu2 [5 208 B]                                                                                                          
Пол:32 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc-dev-bin amd64 2.31-0ubuntu9.2 [71,8 kB]                                                                                          
Пол:33 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 linux-libc-dev amd64 5.4.0-91.102 [1 127 kB]                                                                                          
Пол:34 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libcrypt-dev amd64 1:4.4.10-10ubuntu4 [104 kB]                                                                                                
Пол:35 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 libc6-dev amd64 2.31-0ubuntu9.2 [2 520 kB]                                                                                            
Пол:36 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libsdl-ttf2.0-0 amd64 2.0.11-6 [15,1 kB]                                                                                                  
Пол:37 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 make amd64 4.2.1-1.2 [162 kB]                                                                                                                 
Пол:38 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 manpages-dev all 5.05-1 [2 266 kB]                                                                                                            
Пол:39 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 qt5-gtk-platformtheme amd64 5.12.8+dfsg-0ubuntu1 [124 kB]                                                                                 
Пол:40 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 qttranslations5-l10n all 5.12.8-0ubuntu1 [1 486 kB]                                                                                       
Получено 128 MB за 37с (3 491 kB/s)                                                                                                                                                                       
Извлекаются шаблоны из пакетов: 100%
Предварительная настройка пакетов …
Выбор ранее не выбранного пакета libdouble-conversion3:amd64.
(Чтение базы данных … на данный момент установлено 190170 файлов и каталогов.)
Подготовка к распаковке …/00-libdouble-conversion3_3.1.5-4ubuntu1_amd64.deb …
Распаковывается libdouble-conversion3:amd64 (3.1.5-4ubuntu1) …
Выбор ранее не выбранного пакета libpcre2-16-0:amd64.
Подготовка к распаковке …/01-libpcre2-16-0_10.34-7_amd64.deb …
Распаковывается libpcre2-16-0:amd64 (10.34-7) …
Выбор ранее не выбранного пакета libqt5core5a:amd64.
Подготовка к распаковке …/02-libqt5core5a_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5core5a:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5dbus5:amd64.
Подготовка к распаковке …/03-libqt5dbus5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5dbus5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5network5:amd64.
Подготовка к распаковке …/04-libqt5network5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5network5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libxcb-xinerama0:amd64.
Подготовка к распаковке …/05-libxcb-xinerama0_1.14-2_amd64.deb …
Распаковывается libxcb-xinerama0:amd64 (1.14-2) …
Выбор ранее не выбранного пакета libxcb-xinput0:amd64.
Подготовка к распаковке …/06-libxcb-xinput0_1.14-2_amd64.deb …
Распаковывается libxcb-xinput0:amd64 (1.14-2) …
Выбор ранее не выбранного пакета libqt5gui5:amd64.
Подготовка к распаковке …/07-libqt5gui5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5gui5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5widgets5:amd64.
Подготовка к распаковке …/08-libqt5widgets5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5widgets5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5svg5:amd64.
Подготовка к распаковке …/09-libqt5svg5_5.12.8-0ubuntu1_amd64.deb …
Распаковывается libqt5svg5:amd64 (5.12.8-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5opengl5:amd64.
Подготовка к распаковке …/10-libqt5opengl5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5opengl5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5printsupport5:amd64.
Подготовка к распаковке …/11-libqt5printsupport5_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается libqt5printsupport5:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета libqt5x11extras5:amd64.
Подготовка к распаковке …/12-libqt5x11extras5_5.12.8-0ubuntu1_amd64.deb …
Распаковывается libqt5x11extras5:amd64 (5.12.8-0ubuntu1) …
Выбор ранее не выбранного пакета libsdl1.2debian:amd64.
Подготовка к распаковке …/13-libsdl1.2debian_1.2.15+dfsg2-5_amd64.deb …
Распаковывается libsdl1.2debian:amd64 (1.2.15+dfsg2-5) …
Выбор ранее не выбранного пакета virtualbox-6.1.
Подготовка к распаковке …/14-virtualbox-6.1_6.1.30-148432~Ubuntu~eoan_amd64.deb …
Распаковывается virtualbox-6.1 (6.1.30-148432~Ubuntu~eoan) …
Выбор ранее не выбранного пакета binutils-common:amd64.
Подготовка к распаковке …/15-binutils-common_2.34-6ubuntu1.3_amd64.deb …
Распаковывается binutils-common:amd64 (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета libbinutils:amd64.
Подготовка к распаковке …/16-libbinutils_2.34-6ubuntu1.3_amd64.deb …
Распаковывается libbinutils:amd64 (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета libctf-nobfd0:amd64.
Подготовка к распаковке …/17-libctf-nobfd0_2.34-6ubuntu1.3_amd64.deb …
Распаковывается libctf-nobfd0:amd64 (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета libctf0:amd64.
Подготовка к распаковке …/18-libctf0_2.34-6ubuntu1.3_amd64.deb …
Распаковывается libctf0:amd64 (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета binutils-x86-64-linux-gnu.
Подготовка к распаковке …/19-binutils-x86-64-linux-gnu_2.34-6ubuntu1.3_amd64.deb …
Распаковывается binutils-x86-64-linux-gnu (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета binutils.
Подготовка к распаковке …/20-binutils_2.34-6ubuntu1.3_amd64.deb …
Распаковывается binutils (2.34-6ubuntu1.3) …
Выбор ранее не выбранного пакета libitm1:amd64.
Подготовка к распаковке …/21-libitm1_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается libitm1:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libatomic1:amd64.
Подготовка к распаковке …/22-libatomic1_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается libatomic1:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libasan5:amd64.
Подготовка к распаковке …/23-libasan5_9.3.0-17ubuntu1~20.04_amd64.deb …
Распаковывается libasan5:amd64 (9.3.0-17ubuntu1~20.04) …
Выбор ранее не выбранного пакета liblsan0:amd64.
Подготовка к распаковке …/24-liblsan0_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается liblsan0:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libtsan0:amd64.
Подготовка к распаковке …/25-libtsan0_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается libtsan0:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libubsan1:amd64.
Подготовка к распаковке …/26-libubsan1_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается libubsan1:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libquadmath0:amd64.
Подготовка к распаковке …/27-libquadmath0_10.3.0-1ubuntu1~20.04_amd64.deb …
Распаковывается libquadmath0:amd64 (10.3.0-1ubuntu1~20.04) …
Выбор ранее не выбранного пакета libgcc-9-dev:amd64.
Подготовка к распаковке …/28-libgcc-9-dev_9.3.0-17ubuntu1~20.04_amd64.deb …
Распаковывается libgcc-9-dev:amd64 (9.3.0-17ubuntu1~20.04) …
Выбор ранее не выбранного пакета gcc-9.
Подготовка к распаковке …/29-gcc-9_9.3.0-17ubuntu1~20.04_amd64.deb …
Распаковывается gcc-9 (9.3.0-17ubuntu1~20.04) …
Выбор ранее не выбранного пакета gcc.
Подготовка к распаковке …/30-gcc_4%3a9.3.0-1ubuntu2_amd64.deb …
Распаковывается gcc (4:9.3.0-1ubuntu2) …
Выбор ранее не выбранного пакета libc-dev-bin.
Подготовка к распаковке …/31-libc-dev-bin_2.31-0ubuntu9.2_amd64.deb …
Распаковывается libc-dev-bin (2.31-0ubuntu9.2) …
Выбор ранее не выбранного пакета linux-libc-dev:amd64.
Подготовка к распаковке …/32-linux-libc-dev_5.4.0-91.102_amd64.deb …
Распаковывается linux-libc-dev:amd64 (5.4.0-91.102) …
Выбор ранее не выбранного пакета libcrypt-dev:amd64.
Подготовка к распаковке …/33-libcrypt-dev_1%3a4.4.10-10ubuntu4_amd64.deb …
Распаковывается libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) …
Выбор ранее не выбранного пакета libc6-dev:amd64.
Подготовка к распаковке …/34-libc6-dev_2.31-0ubuntu9.2_amd64.deb …
Распаковывается libc6-dev:amd64 (2.31-0ubuntu9.2) …
Выбор ранее не выбранного пакета libsdl-ttf2.0-0:amd64.
Подготовка к распаковке …/35-libsdl-ttf2.0-0_2.0.11-6_amd64.deb …
Распаковывается libsdl-ttf2.0-0:amd64 (2.0.11-6) …
Выбор ранее не выбранного пакета make.
Подготовка к распаковке …/36-make_4.2.1-1.2_amd64.deb …
Распаковывается make (4.2.1-1.2) …
Выбор ранее не выбранного пакета manpages-dev.
Подготовка к распаковке …/37-manpages-dev_5.05-1_all.deb …
Распаковывается manpages-dev (5.05-1) …
Выбор ранее не выбранного пакета qt5-gtk-platformtheme:amd64.
Подготовка к распаковке …/38-qt5-gtk-platformtheme_5.12.8+dfsg-0ubuntu1_amd64.deb …
Распаковывается qt5-gtk-platformtheme:amd64 (5.12.8+dfsg-0ubuntu1) …
Выбор ранее не выбранного пакета qttranslations5-l10n.
Подготовка к распаковке …/39-qttranslations5-l10n_5.12.8-0ubuntu1_all.deb …
Распаковывается qttranslations5-l10n (5.12.8-0ubuntu1) …
Настраивается пакет manpages-dev (5.05-1) …
Настраивается пакет libdouble-conversion3:amd64 (3.1.5-4ubuntu1) …
Настраивается пакет libxcb-xinput0:amd64 (1.14-2) …
Настраивается пакет binutils-common:amd64 (2.34-6ubuntu1.3) …
Настраивается пакет linux-libc-dev:amd64 (5.4.0-91.102) …
Настраивается пакет libctf-nobfd0:amd64 (2.34-6ubuntu1.3) …
Настраивается пакет libpcre2-16-0:amd64 (10.34-7) …
Настраивается пакет libasan5:amd64 (9.3.0-17ubuntu1~20.04) …
Настраивается пакет libxcb-xinerama0:amd64 (1.14-2) …
Настраивается пакет qttranslations5-l10n (5.12.8-0ubuntu1) …
Настраивается пакет make (4.2.1-1.2) …
Настраивается пакет libquadmath0:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libsdl1.2debian:amd64 (1.2.15+dfsg2-5) …
Настраивается пакет libatomic1:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libqt5core5a:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libubsan1:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libqt5dbus5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libcrypt-dev:amd64 (1:4.4.10-10ubuntu4) …
Настраивается пакет libsdl-ttf2.0-0:amd64 (2.0.11-6) …
Настраивается пакет libbinutils:amd64 (2.34-6ubuntu1.3) …
Настраивается пакет libc-dev-bin (2.31-0ubuntu9.2) …
Настраивается пакет liblsan0:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libitm1:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libtsan0:amd64 (10.3.0-1ubuntu1~20.04) …
Настраивается пакет libctf0:amd64 (2.34-6ubuntu1.3) …
Настраивается пакет libqt5network5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libgcc-9-dev:amd64 (9.3.0-17ubuntu1~20.04) …
Настраивается пакет libc6-dev:amd64 (2.31-0ubuntu9.2) …
Настраивается пакет binutils-x86-64-linux-gnu (2.34-6ubuntu1.3) …
Настраивается пакет libqt5gui5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libqt5widgets5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет binutils (2.34-6ubuntu1.3) …
Настраивается пакет qt5-gtk-platformtheme:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libqt5printsupport5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет libqt5opengl5:amd64 (5.12.8+dfsg-0ubuntu1) …
Настраивается пакет gcc-9 (9.3.0-17ubuntu1~20.04) …
Настраивается пакет libqt5x11extras5:amd64 (5.12.8-0ubuntu1) …
Настраивается пакет libqt5svg5:amd64 (5.12.8-0ubuntu1) …
Настраивается пакет gcc (4:9.3.0-1ubuntu2) …
Настраивается пакет virtualbox-6.1 (6.1.30-148432~Ubuntu~eoan) …
Добавляется группа «vboxusers» (GID 134) ...
Готово.
Обрабатываются триггеры для mime-support (3.64ubuntu1) …
Обрабатываются триггеры для hicolor-icon-theme (0.17-2) …
Обрабатываются триггеры для gnome-menus (3.36.0-1ubuntu1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.2) …
Обрабатываются триггеры для systemd (245.4-4ubuntu3.13) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для shared-mime-info (1.15-1) …
Обрабатываются триггеры для desktop-file-utils (0.24-1ubuntu3) …
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 

```
```yml
oot@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# type virtualbox
virtualbox является /usr/bin/virtualbox
```
```yml
root@PC-Ubuntu:/etc/apt# whereis virtualbox
virtualbox: /usr/bin/virtualbox /usr/lib/virtualbox /usr/share/virtualbox
```
```yml
root@PC-Ubuntu:/etc/apt# man virtualbox
Нет справочной страницы для virtualbox
```
```yml
root@PC-Ubuntu:/etc/apt# mc

Команда «mc» не найдена, но может быть установлена с помощью:

apt install mc

```
```yml
root@PC-Ubuntu:/etc/apt# apt install mc
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  libssh2-1 mc-data
Предлагаемые пакеты:
  arj catdvi | texlive-binaries dbview djvulibre-bin epub-utils gv imagemagick libaspell-dev links | w3m | lynx odt2txt python python-boto python-tz
Следующие НОВЫЕ пакеты будут установлены:
  libssh2-1 mc mc-data
Обновлено 0 пакетов, установлено 3 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 1 817 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 7 994 kB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libssh2-1 amd64 1.8.0-2.1build1 [75,4 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 mc-data all 3:4.8.24-2ubuntu1 [1 265 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 mc amd64 3:4.8.24-2ubuntu1 [477 kB]
Получено 1 817 kB за 1с (2 202 kB/s)       
Выбор ранее не выбранного пакета libssh2-1:amd64.
(Чтение базы данных … на данный момент установлено 195585 файлов и каталогов.)
Подготовка к распаковке …/libssh2-1_1.8.0-2.1build1_amd64.deb …
Распаковывается libssh2-1:amd64 (1.8.0-2.1build1) …
Выбор ранее не выбранного пакета mc-data.
Подготовка к распаковке …/mc-data_3%3a4.8.24-2ubuntu1_all.deb …
Распаковывается mc-data (3:4.8.24-2ubuntu1) …
Выбор ранее не выбранного пакета mc.
Подготовка к распаковке …/mc_3%3a4.8.24-2ubuntu1_amd64.deb …
Распаковывается mc (3:4.8.24-2ubuntu1) …
Настраивается пакет mc-data (3:4.8.24-2ubuntu1) …
Настраивается пакет libssh2-1:amd64 (1.8.0-2.1build1) …
Настраивается пакет mc (3:4.8.24-2ubuntu1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.2) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для desktop-file-utils (0.24-1ubuntu3) …
Обрабатываются триггеры для mime-support (3.64ubuntu1) …
Обрабатываются триггеры для hicolor-icon-theme (0.17-2) …
Обрабатываются триггеры для gnome-menus (3.36.0-1ubuntu1) …

```
#### Установка Vagrant
```ps
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# type vagrant
-bash: type: vagrant: не найден
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

Команда «curl» не найдена, но может быть установлена с помощью:

snap install curl  # version 7.80.0, or
apt  install curl  # version 7.68.0-1ubuntu2.7

See 'snap info curl' for additional versions.

gpg: не найдено данных формата OpenPGP.
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# apt  install curl
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие НОВЫЕ пакеты будут установлены:
  curl
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 161 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 412 kB.
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 curl amd64 7.68.0-1ubuntu2.7 [161 kB]
Получено 161 kB за 0с (447 kB/s)
Выбор ранее не выбранного пакета curl.
(Чтение базы данных … на данный момент установлено 195984 файла и каталога.)
Подготовка к распаковке …/curl_7.68.0-1ubuntu2.7_amd64.deb …
Распаковывается curl (7.68.0-1ubuntu2.7) …
Настраивается пакет curl (7.68.0-1ubuntu2.7) …
Обрабатываются триггеры для man-db (2.9.1-1) …
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease                                                                 
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease                                                                                                         
Пол:4 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                                                                   
Сущ:5 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                      
Сущ:6 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                
Пол:7 https://apt.releases.hashicorp.com focal InRelease [9 495 B]                                    
Пол:8 https://apt.releases.hashicorp.com focal/main amd64 Packages [37,8 kB]
Получено 161 kB за 2с (84,3 kB/s)
Чтение списков пакетов… Готово
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# apt-get update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Сущ:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Пол:4 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                                                                                                    
Сущ:5 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Сущ:6 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                                                                                    
Сущ:7 https://apt.releases.hashicorp.com focal InRelease                                                                                                            
Получено 114 kB за 2с (73,0 kB/s)                                          
Чтение списков пакетов… Готово
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# apt-get install vagrant
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие НОВЫЕ пакеты будут установлены:
  vagrant
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 41,5 MB архивов.
После данной операции объём занятого дискового пространства возрастёт на 117 MB.
Пол:1 https://apt.releases.hashicorp.com focal/main amd64 vagrant amd64 2.2.19 [41,5 MB]
Получено 41,5 MB за 15с (2 810 kB/s)                                                                                                                                                                         
Выбор ранее не выбранного пакета vagrant.
(Чтение базы данных … на данный момент установлен 195991 файл и каталог.)
Подготовка к распаковке …/vagrant_2.2.19_amd64.deb …
Распаковывается vagrant (2.2.19) …
Настраивается пакет vagrant (2.2.19) …
root@PC-Ubuntu:/etc/apt# 
root@PC-Ubuntu:/etc/apt# 
```
```ps
root@PC-Ubuntu:/etc/apt# type vagrant
vagrant является /usr/bin/vagrant
```
```ps
root@PC-Ubuntu:/etc/apt# cd
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# ls -l
итого 4
drwxr-xr-x 3 root root 4096 дек  5 13:14 snap
root@PC-Ubuntu:~# 
```
```ps
root@PC-Ubuntu:~# mkdir -p vagrant-project && cd vagrant-project
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# ls -l
итого 0
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# 

```
### Подготовка к запуску на установку Vagrant
#### Создаем директории проектов Vagrant
```ps
root@PC-Ubuntu:~# mkdir -p vagrant-project && cd vagrant-project
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# ls -l
итого 0
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# 
root@PC-Ubuntu:~/vagrant-project# 
```
#### Создаем директории проектов новый ВМ
```ps
root@PC-Ubuntu:~/vagrant-project# mkdir -p Alfa
root@PC-Ubuntu:~/vagrant-project# mkdir -p Betta
root@PC-Ubuntu:~/vagrant-project# 
```
#### В проекте Betta создаем директории ` ansible ` , ` vagrant `
```ps
root@PC-Ubuntu:~/vagrant-project# cd Betta/
root@PC-Ubuntu:~/vagrant-project/Betta# 
root@PC-Ubuntu:~/vagrant-project/Betta# mkdir -p ansible
root@PC-Ubuntu:~/vagrant-project/Betta# mkdir -p vagrant
root@PC-Ubuntu:~/vagrant-project/Betta# 
root@PC-Ubuntu:~/vagrant-project/Betta# cd ansible/
```
#### В директории ` ansible ` проекте Betta создаем файлы ` inventory ` , ` provision.yml `
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# vim inventory
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# vim provision.yml
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# ls -l
итого 8
-rw-r--r-- 1 root root 117 дек  5 15:50 inventory
-rw-r--r-- 1 root root 861 дек  5 15:57 provision.yml
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# cat inventory 
```
```yml
[nodes:children]
manager

[manager]
server1.netology ansible_host=127.0.0.1 ansible_port=20011 ansible_user=vagrant

root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# cat provision.yml 
```
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
#### 
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# cd ..
root@PC-Ubuntu:~/vagrant-project/Betta# cd vagrant/
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vim ansible
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
#### Смотрим статус Vagrant
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant status
A Vagrant environment or target machine is required to run this
command. Run `vagrant init` to create a new Vagrant environment. Or,
get an ID of a target machine from `vagrant global-status` to run
this command on. A final option is to change to a directory with a
Vagrantfile and to try again.
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
#### Инициализируем Vagrant
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# ls -l
итого 8
-rw-r--r-- 1 root root  136 дек  5 15:59 ansible
-rw-r--r-- 1 root root 3010 дек  5 15:59 Vagrantfile
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
####
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# cat Vagrantfile 
```
#### Дефолтный файл Vagrantfile
```yml
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
#### Удаляем дефолтный файл Vagrantfile
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# rm Vagrantfile 
```
#### Создаем новый файл Vagrantfile
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vim Vagrantfile
```
####
```yml
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
#### Запускаем Vagrant для создания новой ВМ
```ps

root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Box 'bento/ubuntu-20.04' could not be found. Attempting to find and install...
    server1.netology: Box Provider: virtualbox
    server1.netology: Box Version: >= 0
==> server1.netology: Loading metadata for box 'bento/ubuntu-20.04'
    server1.netology: URL: https://vagrantcloud.com/bento/ubuntu-20.04
==> server1.netology: Adding box 'bento/ubuntu-20.04' (v202107.28.0) for provider: virtualbox
    server1.netology: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202107.28.0/providers/virtualbox.box
==> server1.netology: Successfully added box 'bento/ubuntu-20.04' (v202107.28.0) for 'virtualbox'!
==> server1.netology: Importing base box 'bento/ubuntu-20.04'...
==> server1.netology: Matching MAC address for NAT networking...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> server1.netology: Setting the name of the VM: server1.netology
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> server1.netology: Clearing any previously set network interfaces...
==> server1.netology: Preparing network interfaces based on configuration...
    server1.netology: Adapter 1: nat
    server1.netology: Adapter 2: hostonly
==> server1.netology: Forwarding ports...
    server1.netology: 22 (guest) => 20011 (host) (adapter 1)
    server1.netology: 22 (guest) => 2222 (host) (adapter 1)
==> server1.netology: Running 'pre-boot' VM customizations...
==> server1.netology: Booting VM...
==> server1.netology: Waiting for machine to boot. This may take a few minutes...
    server1.netology: SSH address: localhost:2222
    server1.netology: SSH username: vagrant
    server1.netology: SSH auth method: private key
    server1.netology: 
    server1.netology: Vagrant insecure key detected. Vagrant will automatically replace
    server1.netology: this with a newly generated keypair for better security.
    server1.netology: 
    server1.netology: Inserting generated public key within guest...
    server1.netology: Removing insecure key from the guest if it's present...
    server1.netology: Key inserted! Disconnecting and reconnecting using new SSH key...
==> server1.netology: Machine booted and ready!
==> server1.netology: Checking for guest additions in VM...
==> server1.netology: Setting hostname...
==> server1.netology: Configuring and enabling network interfaces...
==> server1.netology: Mounting shared folders...
    server1.netology: /vagrant => /root/vagrant-project/Betta/vagrant
==> server1.netology: Running provisioner: ansible...
`playbook` does not exist on the host: /root/vagrant-project/Betta/ansible/provision.yml
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
#### Была остановка в связи с непрваильным расширением файла ` provision.yml `
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant status
Current machine states:

server1.netology          running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun 05 Dec 2021 12:15:42 PM UTC

  System load:  0.08              Processes:             98
  Usage of /:   2.3% of 61.31GB   Users logged in:       0
  Memory usage: 14%               IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%                IPv4 address for eth1: 192.168.56.11


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
vagrant@server1:~$ 
vagrant@server1:~$ 
vagrant@server1:~$ uname -a
Linux server1 5.4.0-80-generic #90-Ubuntu SMP Fri Jul 9 22:49:44 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
vagrant@server1:~$ 
vagrant@server1:~$ cat /etc*release
cat: '/etc*release': No such file or directory
vagrant@server1:~$ 
vagrant@server1:~$ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"
NAME="Ubuntu"
VERSION="20.04.2 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.2 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
vagrant@server1:~$ 
vagrant@server1:~$ 
vagrant@server1:~$ sudo -i
root@server1:~# 
root@server1:~# 
root@server1:~# exit
logout
vagrant@server1:~$ 
vagrant@server1:~$ exit
logout
Connection to localhost closed.
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# ls -l
итого 8
-rw-r--r-- 1 root root  136 дек  5 15:59 ansible
-rw-r--r-- 1 root root 1221 дек  5 16:01 Vagrantfile
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# cd ..
root@PC-Ubuntu:~/vagrant-project/Betta# cd ansible/
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# ls -l
итого 8
-rw-r--r-- 1 root root 117 дек  5 15:50 inventory
-rw-r--r-- 1 root root 861 дек  5 15:57 provision.yaml
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
```
#### Переименовываем ` provision.yaml ` в ` provision.yml `
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# mv provision.yaml provision.yml 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# ls -l
итого 8
-rw-r--r-- 1 root root 117 дек  5 15:50 inventory
-rw-r--r-- 1 root root 861 дек  5 15:57 provision.yml
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
root@PC-Ubuntu:~/vagrant-project/Betta/ansible# 
```
#### Перезапускаем 
```ps
rroot@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant provision
==> server1.netology: Running provisioner: ansible...
Vagrant gathered an unknown Ansible version:


and falls back on the compatibility mode '1.8'.

Alternatively, the compatibility mode can be specified in your Vagrantfile:
https://www.vagrantup.com/docs/provisioning/ansible_common.html#compatibility_mode

    server1.netology: Running ansible-playbook...
The Ansible software could not be found! Please verify
that Ansible is correctly installed on your host system.

If you haven't installed Ansible yet, please install Ansible
on your host system. Vagrant can't do this for you in a safe and
automated way.
Please check https://docs.ansible.com for more information.
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
#### 
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# apt install ansible
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  ieee-data python3-argcomplete python3-crypto python3-distutils python3-dnspython python3-jinja2 python3-jmespath python3-kerberos python3-libcloud python3-netaddr python3-ntlm-auth
  python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm python3-xmltodict
Предлагаемые пакеты:
  cowsay sshpass python-jinja2-doc ipython3 python-netaddr-docs
Следующие НОВЫЕ пакеты будут установлены:
  ansible ieee-data python3-argcomplete python3-crypto python3-distutils python3-dnspython python3-jinja2 python3-jmespath python3-kerberos python3-libcloud python3-netaddr python3-ntlm-auth
  python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm python3-xmltodict
Обновлено 0 пакетов, установлено 17 новых пакетов, для удаления отмечено 0 пакетов, и 3 пакетов не обновлено.
Необходимо скачать 9 866 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 92,0 MB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 python3-jinja2 all 2.10.1-2 [95,5 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 python3-crypto amd64 2.6.1-13ubuntu2 [237 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-distutils all 3.8.10-0ubuntu1~20.04 [141 kB]
Пол:4 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 python3-dnspython all 1.16.0-1build1 [89,1 kB]
Пол:5 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 ieee-data all 20180805.1 [1 589 kB]
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-netaddr all 0.7.19-3ubuntu1 [236 kB]
Пол:7 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 ansible all 2.9.6+dfsg-1 [5 794 kB]
Пол:8 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-argcomplete all 1.8.1-1.3ubuntu1 [27,2 kB]
Пол:9 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-jmespath all 0.9.4-2ubuntu1 [21,5 kB]
Пол:10 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-kerberos amd64 1.1.14-3.1build1 [22,6 kB]
Пол:11 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-libcloud all 2.8.0-1 [1 403 kB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-ntlm-auth all 1.1.0-1 [19,6 kB]
Пол:13 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-requests-kerberos all 0.12.0-2 [11,9 kB]
Пол:14 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-requests-ntlm all 1.1.0-1 [6 004 B]
Пол:15 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-selinux amd64 3.0-1build2 [139 kB]
Пол:16 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-xmltodict all 0.12.0-1 [12,6 kB]
Пол:17 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 python3-winrm all 0.3.0-2 [21,7 kB]
Получено 9 866 kB за 4с (2 272 kB/s)        
Выбор ранее не выбранного пакета python3-jinja2.
(Чтение базы данных … на данный момент установлено 202309 файлов и каталогов.)
Подготовка к распаковке …/00-python3-jinja2_2.10.1-2_all.deb …
Распаковывается python3-jinja2 (2.10.1-2) …
Выбор ранее не выбранного пакета python3-crypto.
Подготовка к распаковке …/01-python3-crypto_2.6.1-13ubuntu2_amd64.deb …
Распаковывается python3-crypto (2.6.1-13ubuntu2) …
Выбор ранее не выбранного пакета python3-distutils.
Подготовка к распаковке …/02-python3-distutils_3.8.10-0ubuntu1~20.04_all.deb …
Распаковывается python3-distutils (3.8.10-0ubuntu1~20.04) …
Выбор ранее не выбранного пакета python3-dnspython.
Подготовка к распаковке …/03-python3-dnspython_1.16.0-1build1_all.deb …
Распаковывается python3-dnspython (1.16.0-1build1) …
Выбор ранее не выбранного пакета ieee-data.
Подготовка к распаковке …/04-ieee-data_20180805.1_all.deb …
Распаковывается ieee-data (20180805.1) …
Выбор ранее не выбранного пакета python3-netaddr.
Подготовка к распаковке …/05-python3-netaddr_0.7.19-3ubuntu1_all.deb …
Распаковывается python3-netaddr (0.7.19-3ubuntu1) …
Выбор ранее не выбранного пакета ansible.
Подготовка к распаковке …/06-ansible_2.9.6+dfsg-1_all.deb …
Распаковывается ansible (2.9.6+dfsg-1) …
Выбор ранее не выбранного пакета python3-argcomplete.
Подготовка к распаковке …/07-python3-argcomplete_1.8.1-1.3ubuntu1_all.deb …
Распаковывается python3-argcomplete (1.8.1-1.3ubuntu1) …
Выбор ранее не выбранного пакета python3-jmespath.
Подготовка к распаковке …/08-python3-jmespath_0.9.4-2ubuntu1_all.deb …
Распаковывается python3-jmespath (0.9.4-2ubuntu1) …
Выбор ранее не выбранного пакета python3-kerberos.
Подготовка к распаковке …/09-python3-kerberos_1.1.14-3.1build1_amd64.deb …
Распаковывается python3-kerberos (1.1.14-3.1build1) …
Выбор ранее не выбранного пакета python3-libcloud.
Подготовка к распаковке …/10-python3-libcloud_2.8.0-1_all.deb …
Распаковывается python3-libcloud (2.8.0-1) …
Выбор ранее не выбранного пакета python3-ntlm-auth.
Подготовка к распаковке …/11-python3-ntlm-auth_1.1.0-1_all.deb …
Распаковывается python3-ntlm-auth (1.1.0-1) …
Выбор ранее не выбранного пакета python3-requests-kerberos.
Подготовка к распаковке …/12-python3-requests-kerberos_0.12.0-2_all.deb …
Распаковывается python3-requests-kerberos (0.12.0-2) …
Выбор ранее не выбранного пакета python3-requests-ntlm.
Подготовка к распаковке …/13-python3-requests-ntlm_1.1.0-1_all.deb …
Распаковывается python3-requests-ntlm (1.1.0-1) …
Выбор ранее не выбранного пакета python3-selinux.
Подготовка к распаковке …/14-python3-selinux_3.0-1build2_amd64.deb …
Распаковывается python3-selinux (3.0-1build2) …
Выбор ранее не выбранного пакета python3-xmltodict.
Подготовка к распаковке …/15-python3-xmltodict_0.12.0-1_all.deb …
Распаковывается python3-xmltodict (0.12.0-1) …
Выбор ранее не выбранного пакета python3-winrm.
Подготовка к распаковке …/16-python3-winrm_0.3.0-2_all.deb …
Распаковывается python3-winrm (0.3.0-2) …
Настраивается пакет python3-distutils (3.8.10-0ubuntu1~20.04) …
Настраивается пакет python3-ntlm-auth (1.1.0-1) …
Настраивается пакет python3-kerberos (1.1.14-3.1build1) …
Настраивается пакет python3-xmltodict (0.12.0-1) …
Настраивается пакет python3-jinja2 (2.10.1-2) …
Настраивается пакет python3-jmespath (0.9.4-2ubuntu1) …
Настраивается пакет python3-requests-kerberos (0.12.0-2) …
Настраивается пакет ieee-data (20180805.1) …
Настраивается пакет python3-dnspython (1.16.0-1build1) …
Настраивается пакет python3-selinux (3.0-1build2) …
Настраивается пакет python3-crypto (2.6.1-13ubuntu2) …
Настраивается пакет python3-argcomplete (1.8.1-1.3ubuntu1) …
Настраивается пакет python3-requests-ntlm (1.1.0-1) …
Настраивается пакет python3-libcloud (2.8.0-1) …
Настраивается пакет python3-netaddr (0.7.19-3ubuntu1) …
Настраивается пакет python3-winrm (0.3.0-2) …
Настраивается пакет ansible (2.9.6+dfsg-1) …
Обрабатываются триггеры для man-db (2.9.1-1) …
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
####
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant provision
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
[WARNING]: Consider using the get_url or uri module rather than running 'curl'.
If you need to use command because get_url or uri is insufficient you can add
'warn: false' to this command task or set 'command_warnings=False' in
ansible.cfg to get rid of this message.
changed: [server1.netology]

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=1   

root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vgrant ssh

Команда «vgrant» не найдена. Возможно, вы имели в виду:

  command 'vagrant' from deb vagrant (2.2.6+dfsg-2ubuntu3)

Try: apt install <deb name>

root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# 
```
```ps
root@PC-Ubuntu:~/vagrant-project/Betta/vagrant# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun 05 Dec 2021 12:28:02 PM UTC

  System load:  0.11              Users logged in:          0
  Usage of /:   3.2% of 61.31GB   IPv4 address for docker0: 172.17.0.1
  Memory usage: 20%               IPv4 address for eth0:    10.0.2.15
  Swap usage:   0%                IPv4 address for eth1:    192.168.56.11
  Processes:    104


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Sun Dec  5 12:25:00 2021 from 10.0.2.2
vagrant@server1:~$ 
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
vagrant@server1:~$ 
vagrant@server1:~$ 
```
####
```ps
vagrant@server1:~$ sudo apt install mc
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libssh2-1 mc-data unzip
Suggested packages:
  arj catdvi | texlive-binaries dbview djvulibre-bin epub-utils genisoimage gv imagemagick libaspell-dev links | w3m | lynx odt2txt poppler-utils python python-boto python-tz xpdf | pdf-viewer zip
The following NEW packages will be installed:
  libssh2-1 mc mc-data unzip
0 upgraded, 4 newly installed, 0 to remove and 102 not upgraded.
Need to get 1,986 kB of archives.
After this operation, 8,587 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal/universe amd64 libssh2-1 amd64 1.8.0-2.1build1 [75.4 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/universe amd64 mc-data all 3:4.8.24-2ubuntu1 [1,265 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/universe amd64 mc amd64 3:4.8.24-2ubuntu1 [477 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/main amd64 unzip amd64 6.0-25ubuntu1 [169 kB]
Fetched 1,986 kB in 1s (1,666 kB/s)
Selecting previously unselected package libssh2-1:amd64.
(Reading database ... 41797 files and directories currently installed.)
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
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
vagrant@server1:~$ 
vagrant@server1:~$ 
vagrant@server1:~$ mc

vagrant@server1:~$ 


```
