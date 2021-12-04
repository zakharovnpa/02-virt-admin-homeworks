
## На ПК Elena-PC установка ansible на Ubuntu-20.04 для возможности конфигурирования новых ВМ совместно с vagrant

#### Создаем новую директорию проекта
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project#mkdir -p /mnt/c/Users/serje/Vagrant-project/server-2
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project# cd server-2
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### Инициализируем vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant init
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# ls -l
total 4
-rwxrwxrwx 1 maestro maestro 3010 Nov 27 12:17 Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### Устнанавливаем ansible
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# apt install ansible
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  ieee-data python3-argcomplete python3-crypto python3-dnspython python3-jmespath python3-kerberos python3-libcloud python3-lockfile
  python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm python3-xmltodict
Suggested packages:
  cowsay sshpass python-lockfile-doc ipython3 python-netaddr-docs
The following NEW packages will be installed:
  ansible ieee-data python3-argcomplete python3-crypto python3-dnspython python3-jmespath python3-kerberos python3-libcloud
  python3-lockfile python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux python3-winrm
  python3-xmltodict
0 upgraded, 16 newly installed, 0 to remove and 251 not upgraded.
Need to get 9644 kB of archives.
After this operation, 90.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-crypto amd64 2.6.1-13ubuntu2 [237 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-dnspython all 1.16.0-1build1 [89.1 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main amd64 ieee-data all 20180805.1 [1589 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-netaddr all 0.7.19-3ubuntu1 [236 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/universe amd64 ansible all 2.9.6+dfsg-1 [5794 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-argcomplete all 1.8.1-1.3ubuntu1 [27.2 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 python3-jmespath all 0.9.4-2ubuntu1 [21.5 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-kerberos amd64 1.1.14-3.1build1 [22.6 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal/main amd64 python3-lockfile all 1:0.12.2-2ubuntu2 [14.6 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-libcloud all 2.8.0-1 [1403 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-ntlm-auth all 1.1.0-1 [19.6 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-requests-kerberos all 0.12.0-2 [11.9 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-requests-ntlm all 1.1.0-1 [6004 B]
Get:14 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-selinux amd64 3.0-1build2 [139 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-xmltodict all 0.12.0-1 [12.6 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal/universe amd64 python3-winrm all 0.3.0-2 [21.7 kB]
Fetched 9644 kB in 10s (944 kB/s)
Selecting previously unselected package python3-crypto.
(Reading database ... 38571 files and directories currently installed.)
Preparing to unpack .../00-python3-crypto_2.6.1-13ubuntu2_amd64.deb ...
Unpacking python3-crypto (2.6.1-13ubuntu2) ...
Selecting previously unselected package python3-dnspython.
Preparing to unpack .../01-python3-dnspython_1.16.0-1build1_all.deb ...
Unpacking python3-dnspython (1.16.0-1build1) ...
Selecting previously unselected package ieee-data.
Preparing to unpack .../02-ieee-data_20180805.1_all.deb ...
Unpacking ieee-data (20180805.1) ...
Selecting previously unselected package python3-netaddr.
Preparing to unpack .../03-python3-netaddr_0.7.19-3ubuntu1_all.deb ...
Unpacking python3-netaddr (0.7.19-3ubuntu1) ...
Selecting previously unselected package ansible.
Preparing to unpack .../04-ansible_2.9.6+dfsg-1_all.deb ...
Unpacking ansible (2.9.6+dfsg-1) ...
Selecting previously unselected package python3-argcomplete.
Preparing to unpack .../05-python3-argcomplete_1.8.1-1.3ubuntu1_all.deb ...
Unpacking python3-argcomplete (1.8.1-1.3ubuntu1) ...
Selecting previously unselected package python3-jmespath.
Preparing to unpack .../06-python3-jmespath_0.9.4-2ubuntu1_all.deb ...
Unpacking python3-jmespath (0.9.4-2ubuntu1) ...
Selecting previously unselected package python3-kerberos.
Preparing to unpack .../07-python3-kerberos_1.1.14-3.1build1_amd64.deb ...
Unpacking python3-kerberos (1.1.14-3.1build1) ...
Selecting previously unselected package python3-lockfile.
Preparing to unpack .../08-python3-lockfile_1%3a0.12.2-2ubuntu2_all.deb ...
Unpacking python3-lockfile (1:0.12.2-2ubuntu2) ...
Selecting previously unselected package python3-libcloud.
Preparing to unpack .../09-python3-libcloud_2.8.0-1_all.deb ...
Unpacking python3-libcloud (2.8.0-1) ...
Selecting previously unselected package python3-ntlm-auth.
Preparing to unpack .../10-python3-ntlm-auth_1.1.0-1_all.deb ...
Unpacking python3-ntlm-auth (1.1.0-1) ...
Selecting previously unselected package python3-requests-kerberos.
Preparing to unpack .../11-python3-requests-kerberos_0.12.0-2_all.deb ...
Unpacking python3-requests-kerberos (0.12.0-2) ...
Selecting previously unselected package python3-requests-ntlm.
Preparing to unpack .../12-python3-requests-ntlm_1.1.0-1_all.deb ...
Unpacking python3-requests-ntlm (1.1.0-1) ...
Selecting previously unselected package python3-selinux.
Preparing to unpack .../13-python3-selinux_3.0-1build2_amd64.deb ...
Unpacking python3-selinux (3.0-1build2) ...
Selecting previously unselected package python3-xmltodict.
Preparing to unpack .../14-python3-xmltodict_0.12.0-1_all.deb ...
Unpacking python3-xmltodict (0.12.0-1) ...
Selecting previously unselected package python3-winrm.
Preparing to unpack .../15-python3-winrm_0.3.0-2_all.deb ...
Unpacking python3-winrm (0.3.0-2) ...
Setting up python3-lockfile (1:0.12.2-2ubuntu2) ...
Setting up python3-ntlm-auth (1.1.0-1) ...
Setting up python3-kerberos (1.1.14-3.1build1) ...
Setting up python3-xmltodict (0.12.0-1) ...
Setting up python3-jmespath (0.9.4-2ubuntu1) ...
Setting up python3-requests-kerberos (0.12.0-2) ...
Setting up ieee-data (20180805.1) ...
Setting up python3-dnspython (1.16.0-1build1) ...
Setting up python3-selinux (3.0-1build2) ...
Setting up python3-crypto (2.6.1-13ubuntu2) ...
Setting up python3-argcomplete (1.8.1-1.3ubuntu1) ...
Setting up python3-requests-ntlm (1.1.0-1) ...
Setting up python3-libcloud (2.8.0-1) ...
Setting up python3-netaddr (0.7.19-3ubuntu1) ...
Setting up python3-winrm (0.3.0-2) ...
Setting up ansible (2.9.6+dfsg-1) ...
Processing triggers for man-db (2.9.1-1) ...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### Статус vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### Создаем в директории нового проекта server-2 окружение для запуска ВМ под управлением vagrant & ansible
* Файл Vagrantfile
```ruby
# -*- mode: ruby -*-

ISO = "bento/ubuntu-20.04"
#NET = "192.168.192."
DOMAIN = ".netology"
HOST_PREFIX = "server"
INVENTORY_PATH = "../ansible/inventory"

servers = [
  {
    :hostname => HOST_PREFIX + "1" + DOMAIN,
    #:ip => NET + "11",
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

#### Проверяем какой дитсрибутив доступен для создания ВМ
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant box list
bento/ubuntu-20.04 (virtualbox, 202107.28.0)
```

#### Добавляем переменную
```bash
echo 'export VAGRANT_DEFAULT_PROVIDER=virtualbox' >> ~/.bashrc
```
#### Перезапускаем bashrc
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#source ~/.bashrc
```
#### Проверяем окружение
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#env
```
#### Запускаем новую ВМ
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Importing base box 'bento/ubuntu-20.04'...
==> server1.netology: Matching MAC address for NAT networking...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> server1.netology: Setting the name of the VM: server1.netology
==> server1.netology: Clearing any previously set network interfaces...
Network settings specified in your Vagrantfile define an invalid
IP address. Please review the error message below and update your
Vagrantfile network settings:

  Address:
  Netmask:
  Error: address family must be specified
  ```
  #### Исправляем файл ` Vagrantfile `. Устанавливаем IP адреса
  ```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant status
Current machine states:

server1.netology          poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> server1.netology: Clearing any previously set network interfaces...
The IP address configured for the host-only network is not within the
allowed ranges. Please update the address used to be within the allowed
ranges and run the command again.

  Address: 192.168.192.11
  Ranges: 192.168.56.0/21

Valid ranges can be modified in the /etc/vbox/networks.conf file. For
more information including valid format see:

  https://www.virtualbox.org/manual/ch06.html#network_hostonly
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### В файле ` Vagrentfile ` выставляем ip адрес внутренней сети Virtualbox для новой ВМ
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vim Vagrantfile
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### Перезапускаем vagrant
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
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
    server1.netology: /vagrant => /mnt/c/Users/serje/Vagrant-project/server-2

==> server1.netology: Running provisioner: ansible...
`playbook` does not exist on the host: /mnt/c/Users/serje/Vagrant-project/ansible/provision.yml
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```
#### К новой ВМ можно подключиться по ssh
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant ssh
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat 27 Nov 2021 10:52:17 AM UTC

  System load:  0.08              Processes:             98
  Usage of /:   2.4% of 61.31GB   Users logged in:       0
  Memory usage: 15%               IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%                IPv4 address for eth1: 192.168.56.11


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
vagrant@server1:~$
vagrant@server1:~$
```
#### Удаляем новую ВМ
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant status
Current machine states:

server1.netology          running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant halt
==> server1.netology: Attempting graceful shutdown of VM...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant status
Current machine states:

server1.netology          poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant destroy
    server1.netology: Are you sure you want to destroy the 'server1.netology' VM? [y/N] y
==> server1.netology: Destroying VM and associated drives...
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant status
Current machine states:

server1.netology          not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```

#### Создаем директорию` /ansible ` в директории с проектами Vagrant ` ../Vagrant-project/ansible/ ` и создаем в ней файл ` inventory ` с содержимым:
```bash
[nodes:children]
manager

[manager]
server1.netology ansible_host=127.0.0.1 ansible_port=20011 ansible_user=vagrant
```
#### В директории ` /ansible `, находящейся в дирктории с проектами Vagrant ` ../Vagrant-project/ansible/ ` создаем файл ` provision.yml ` с содержимым. 

* Строго соблюдать отступы. точно как в этом файле.
* Проверить директорию ` ~/.ssh/ ` на содержимое. Там должен быть файл ` id_rsa.pub `
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
#### Пример неверно написанного файла. 
#### При этом после запуска команды ` vagrant provision ` появляются синтаксические ошибки:
* Ошибка 1:
```bash
ERROR! Syntax Error while loading YAML.
  mapping values are not allowed in this context

The error appears to be in '/mnt/c/Users/serje/Vagrant-project/ansible/provision.yml': line 2, column 11, but may
be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:

- hosts: nodes
    become: yes
          ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 2:
```bash
ERROR! this task 'apt' has extra params, which is only allowed in the following modules: include_tasks, import_tasks, include, import_role, script, raw, shell, include_vars, add_host, win_command, command, group_by, set_fact, meta, win_shell, include_role

The error appears to be in '/mnt/c/Users/serje/Vagrant-project/ansible/provision.yml': line 19, column 7, but may
be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:


    - name: Installing tools
      ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 1:
```bash

ERROR! this task 'apt' has extra params, which is only allowed in the following modules: script, include, command, win_shell, include_role, raw, meta, win_command, include_tasks, group_by, include_vars, shell, import_role, add_host, import_tasks, set_fact

The error appears to be in '/mnt/c/Users/serje/Vagrant-project/ansible/provision.yml': line 19, column 7, but may
be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:


    - name: Installing tools
      ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 3:
```bash
...
he offending line appears to be:


 tasks:
 ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 4:
```bash
The offending line appears to be:

  - name: Create directory for ssh-keys
   file: state=directory mode=0700 dest=/root/.ssh/
   ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 5:
```bash
The offending line appears to be:

  - name: Create directory for ssh-keys
      file: state=directory mode=0700 dest=/root/.ssh/
          ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
* Ошибка 6:
```bash
he offending line appears to be:

      update_cache=yes
                  ^ here

```
* Ошибка 7:
```bash
he offending line appears to be:


  - name: Adding rsa-key in /root/.ssh/authorized_keys
    ^ here
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
#### Пример неверно расположенных отступов в синтаксисе файла?
```yml
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
#### Если ВМ уже ране была создана и запущена, то можно запустить ее конфигурирование с помощью команды ` vagrant provision `
```bash
root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2# vagrant provision
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

root@DESKTOP-FMD4BBS:/mnt/c/Users/serje/Vagrant-project/server-2#
```

#### В итоге запущена новая ВМ и с помошью ansible playbook (provision.yml) установлены Curl, Git, Dicker
```bash
vagrant@server1:~$
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
vagrant@server1:~$
vagrant@server1:~$ vagrant --version
-bash: vagrant: command not found
vagrant@server1:~$
vagrant@server1:~$
vagrant@server1:~$ whereis docker
docker: /usr/bin/docker /etc/docker /usr/libexec/docker /usr/share/man/man1/docker.1.gz
vagrant@server1:~$
vagrant@server1:~$ whereis curl
curl: /usr/bin/curl /usr/share/man/man1/curl.1.gz
vagrant@server1:~$
vagrant@server1:~$ whereis git
git: /usr/bin/git /usr/share/man/man1/git.1.gz
vagrant@server1:~$
```
