## На ПК Elena-PC в Ubuntu на WSL. Старт новой ВМ по принципу IaaS с помощью Vagrant & Ansible и установка в ней Docker
### Вход в ОС Ubuntu на WSL
```ps
Windows PowerShell
(C) Корпорация Майкрософт (Microsoft Corporation). Все права защищены.

Попробуйте новую кроссплатформенную оболочку PowerShell (https://aka.ms/pscore6)

PS C:\Windows\system32>
PS C:\Windows\system32>
PS C:\Windows\system32> wsl --status
Распределение по умолчанию: Ubuntu-20.04
Версия по умолчанию: 2
Включите функцию Windows для платформы виртуальных машин и убедитесь в том, что в BIOS включена виртуализация.
Дополнительные сведения см. на странице https://aka.ms/wsl2-install
PS C:\Windows\system32>
PS C:\Windows\system32> wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-20.04    Stopped         1
PS C:\Windows\system32>
PS C:\Windows\system32> wsl
maestro@DESKTOP-FMD4BBS:/mnt/c/Windows/system32$
maestro@DESKTOP-FMD4BBS:/mnt/c/Windows/system32$ sudo -i
[sudo] password for maestro:
root@DESKTOP-FMD4BBS:~#
```
### Создаем директорию нового проекта Betta
```ps
root@DESKTOP-FMD4BBS:~# cd /mnt/c/Users/serje/Vagrant-project/Betta/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta# mc

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta# cd ..
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project# cd Alfa/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# ls -lha
total 4.0K
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:59 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 11:21 ..
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 09:46 .vagrant
-rwxrwxrwx 1 maestro maestro 3.0K Dec  1 09:59 Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Alfa# cd ..
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project# cd Betta/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta# ls -lha
total 0
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 13:05 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 11:21 ..
drwxrwxrwx 1 maestro maestro 4.0K Nov 27 13:15 ansible
-rwxrwxrwx 1 maestro maestro  135 Nov 27 13:19 ansible.cfg
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
```
#### Создаем директорию vagrant, в которой будем инициализировать новую ВМ
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta# mkdir -p vagrant
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta# cd vagrant/
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant status
A Vagrant environment or target machine is required to run this
command. Run `vagrant init` to create a new Vagrant environment. Or,
get an ID of a target machine from `vagrant global-status` to run
this command on. A final option is to change to a directory with a
Vagrantfile and to try again.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
```
#### Инициализируем Vagrant. Создается дефолтный Vagrantfile и скрытые директории Vagranta
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# ls -lha
total 4.0K
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 13:08 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 13:08 ..
-rwxrwxrwx 1 maestro maestro 3.0K Dec  1 13:08 Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
```
#### Редактируем Vagrantfile по своим задачам
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# mc


root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# mc


root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# ls -lha
total 4.0K
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 13:16 .
drwxrwxrwx 1 maestro maestro 4.0K Dec  1 13:08 ..
-rwxrwxrwx 1 maestro maestro 1.3K Dec  1 13:15 Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# mc


root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# mc
```
### Проверяем работоспособность Vagrant. Должен показать версию ПО и свой статус.
```ps

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant --version
Vagrant 2.2.19
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant status
Current machine states:

server1.netology          not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
# Также нужно посмотреть vagrant ssh-config
```
### Запускаем создание новой ВМ
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Importing base box 'bento/ubuntu-20.04'...
==> server1.netology: Matching MAC address for NAT networking...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> server1.netology: Setting the name of the VM: server1.netology
==> server1.netology: Clearing any previously set network interfaces...
==> server1.netology: Preparing network interfaces based on configuration...
    server1.netology: Adapter 1: nat
    server1.netology: Adapter 2: hostonly
==> server1.netology: Forwarding ports...
    server1.netology: 22 (guest) => 20011 (host) (adapter 1)
    server1.netology: 22 (guest) => 2222 (host) (adapter 1)
    server1.netology: 22 (guest) => 2222 (host) (adapter 1)
==> server1.netology: Running 'pre-boot' VM customizations...
==> server1.netology: Booting VM...
==> server1.netology: Waiting for machine to boot. This may take a few minutes...
    server1.netology: SSH address: localhost:2222
    server1.netology: SSH username: vagrant
    server1.netology: SSH auth method: private key
    server1.netology: Warning: Remote connection disconnect. Retrying...
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
    server1.netology: /vagrant => /mnt/c/Users/serje/Vagrant-project/Betta/vagrant
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...
[WARNING]: Ansible is being run in a world writable directory
(/mnt/c/Users/serje/Vagrant-project/Betta/vagrant), ignoring it as an
ansible.cfg source. For more information see
https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-
world-writable-dir
ERROR! Syntax Error while loading YAML.
  mapping values are not allowed in this context

The error appears to be in '/mnt/c/Users/serje/Vagrant-project/Betta/ansible/provision.yml': line 2, column 11, but may
be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:

- hosts: nodes
    become: yes
          ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
```
### Необходимо исправить синтаксические ошибки. Неверные отступы.
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# mc
```
### Перезапускаем процесс обеспечения новой ВМ сервисами ` vagrant provision `
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant provision
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...
[WARNING]: Ansible is being run in a world writable directory
(/mnt/c/Users/serje/Vagrant-project/Betta/vagrant), ignoring it as an
ansible.cfg source. For more information see
https://docs.ansible.com/ansible/devel/reference_appendices/config.html#cfg-in-
world-writable-dir

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

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant#
```
### Подключаемся к новой ВМ и смотрим, что выполнена установка Docker
```ps
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/Betta/vagrant# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed 01 Dec 2021 09:48:12 AM UTC

  System load:  0.16              Users logged in:          0
  Usage of /:   3.2% of 61.31GB   IPv4 address for docker0: 172.17.0.1
  Memory usage: 19%               IPv4 address for eth0:    10.0.2.15
  Swap usage:   0%                IPv4 address for eth1:    192.168.56.11
  Processes:    101


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Wed Dec  1 09:42:30 2021 from 10.0.2.2
vagrant@server1:~$
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
vagrant@server1:~$
vagrant@server1:~$
```

