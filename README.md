# Ubuntu Machine Setup

After new setup, it becomes clumsy to setup packages. It is possible that you can forget. This repo will contain all the packages used after a fresh 
Ubuntu machine setup or if new packages needed to be setup.

Current OS
```
Distributor ID: Ubuntu
Description:    Ubuntu 19.10
Release:        19.10
Codename:       eoan
```

### Ansible vault

* Create a file named - `.ansible-vault.txt` in the `$HOME` folder and add your own Ansible vault password in there
```
$ touch $HOME/.ansible-vault.txt
```

* Create a file named - `vault` in the `group_vars/all` folder that holds the secrets, and add the necessary secrets in there. Template of the vault 
file
```
---

# local escalation and user/pass
ansible_become: yes
ansible_become_user: <your-root-user>
ansible_become_password: <your-root-password>

ansible_ssh_user: <your-ssh-user>      # that is your own user
ansible_ssh_pass: <your-ssh-password>  # that is your own password
```

* Now encrypt the vault
```
$ ansible-vault encrypt group_vars/all/vault
```

* View the vault
```
$ ansible-vault view group_vars/all/vault
```

### How to Run

```
$ ansible-playbook playbook.yaml
```

Or, in case of a particular setup use `tags`

```
ansible-playbook playbook.yaml --tags "docker"
```

### TODO
List of the packages planned to install
1. Java
2. Google chrome
3. etc.