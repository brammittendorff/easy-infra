# Easy Infra

## Setup

### Create inventory file

To authenticate with a user and pass please create an `hosts` file and add contents:

```
[ovh-webservers]
kimsufi-host-1 ansible_host=127.0.0.1 ansible_password=password

[ovh-mailservers]
kimsufi-host-2 ansible_host=127.0.0.1 ansible_password=password

[webservers:children]
ovh-webservers

[mailservers:children]
ovh-mailservers

[all:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
ansible_connection=ssh
ansible_user=user
ansible_become=yes
ansible_python_interpreter='/usr/bin/python3'
```

### Install ansible galaxy dependencies

```
ansible-galaxy install -r requirements.yml 
```

## Execute

### Do a ping against all servers

To ping execute:

```
ansible -i hosts all -m ping
```

### Run webserver roles

```
ansible-playbook -i hosts playbooks/webservers.yml
```