
## Установка ansible на Ubuntu-20.04 для возможности конфигурирования новых ВМ совместно с vagrant

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


#### Создаем директорию  ` ../ansible/ ` и создаем в ней файл ` inventory ` с содержимым:
```bash
[nodes:children]
manager

[manager]
server1.netology ansible_host=127.0.0.1 ansible_port=20011 ansible_user=vagrant
```
#### В директории  ` ../ansible/ ` создаем файл ` provision.yml ` с содержимым:
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
