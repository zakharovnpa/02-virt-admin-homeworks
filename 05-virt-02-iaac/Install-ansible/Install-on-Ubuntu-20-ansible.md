
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


