# 1. Zabbix Configuration Management with Ansible Roles

Table of Contents:
- [1. Zabbix Configuration Management with Ansible Roles](#1-zabbix-configuration-management-with-ansible-roles)
  - [1.1. Requirement](#11-requirement)
  - [1.2. Steps for Setup Zabbix with Ansible](#12-steps-for-setup-zabbix-with-ansible)
    - [1.2.1. Edit file `hosts` and adjust the following section with your Servers.](#121-edit-file-hosts-and-adjust-the-following-section-with-your-servers)
    - [1.2.2. Connection Test all Hosts Inventory](#122-connection-test-all-hosts-inventory)
    - [1.2.3. Execute Ansible Playbook](#123-execute-ansible-playbook)


## 1.1. Requirement
- 2 Server [CentOS-8]
  - Zabbix Server 5.0
  - MySQL Server 8.0
- Ansible Machine (Server Base / Localhost)

**Note:** For easy Provisioning 2 server above (LAB). You can use the Vagrant and VirtualBox with the [Vagrantfile](Vagrantfile)


## 1.2. Steps for Setup Zabbix with Ansible

### 1.2.1. Edit file `hosts` and adjust the following section with your Servers.
- ansible_host
- ansible_user
- ansible_ssh_private_key_file

```
[all:vars]

[zabbix]
zabbix1 ansible_host=192.168.99.21 ansible_user=vagrant ansible_ssh_private_key_file=~/.vagrant.d/insecure_private_key ansible_ssh_common_args='-o StrictHostKeyChecking=no'

[database]
database1 ansible_host=192.168.99.31 ansible_user=vagrant ansible_ssh_private_key_file=~/.vagrant.d/insecure_private_key ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```


### 1.2.2. Connection Test all Hosts Inventory
Test ping:
```
ansible all -i hosts -m ping
```

Result if Success:
```
zabbix1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
database1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
```

### 1.2.3. Execute Ansible Playbook
If you ready :D. Go go go...
```
ansible-playbook -i hosts main.yaml
```