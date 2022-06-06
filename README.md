# Ubuntu Machine Setup

After new Ubuntu setup, it becomes clumsy to setup software. It is possible to forget the necessary packages
installed. We can use Ansible to provision the Ubuntu machine with the required software's.

Current OS

```
Distributor ID: Ubuntu
Description:    Ubuntu 20.04 LTS
Release:        20.04
Codename:       focal
```

Copy the `inventory/ubuntu.ini.template` to `inventory/ubuntu.ini` and put the relevant information

```sh
$ cp inventory/ubuntu.ini.template inventory/ubuntu.ini
```

Install the required package

```sh
$ pip install -r requirements.txt
```

Run the below command to check that the the host is connected

```sh
$ ansible -i inventory/ubuntu.ini -m ping all
```

### How to Run

Use the below command to run the playbook

```
$ ansible-playbook -i inventory/ubuntu.ini ubuntu-provision.yaml
```

Or, in case of a particular setup use `tags`

```
$ ansible-playbook -i inventory/ubuntu.ini ubuntu-provision.yaml --tags "docker"
```

### Prerequisites

Before running the playbook, `ansible` needs to be installed. For this use the below command

```sh
pip install -r requirements.txt
```

Also the SSH user (the `ansible_user` ) needs to be in the `sudoers` file, f.e. if `ansible` is the SSH user

```sh
touch /etc/sudoers.d/ansible
echo "ansible  ALL=(ALL:ALL) ALL" > /etc/sudoers.d/ansible
chown 640 /etc/sudoers.d/ansible
```

### List of roles

Below are the list of softwares or packages that could be installed

* Java
* Docker

### Testing

For the testing, `Vagrant` is used. There is already `Vagrantfile`. Use the `up` command to start the VM

```sh
$ vagrant up
```

Use the `vagrant ssh-config` command to check the necessary SSH configuration

```sh
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2200
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/ghost016/DevOps_Workspace/Ansible/ubuntu-provision/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL

$ ssh vagrant@127.0.0.1 -p 2200 -i .vagrant/machines/default/virtualbox/private_key
```

Update the information in the `inventory/vagrant.ini` as per the SSH config above

```ini
[vagrant]
test.hadoop.com ansible_port=2200

[vagrant:vars]
ansible_host=127.0.0.1
ansible_user=vagrant
ansible_become=yes
ansible_private_key_file=.vagrant/machines/default/virtualbox/private_key
```

Check that the Ansible is able to connect to the Vagrant machine

```sh
$ ansible -m ping all
```
