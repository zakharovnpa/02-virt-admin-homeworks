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
