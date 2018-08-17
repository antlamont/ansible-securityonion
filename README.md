# Ansible playbooks for Security Onion deployment

The purpose of this project is to facilitate the deployment and management of a Security Onion cluster using Ansible.

## Getting Started

Security Onion v16.04.4.1 introduced a new architecture, and I strongly recommend to read the [Security Onion Wiki](https://github.com/Security-Onion-Solutions/security-onion/wiki) before using these playbooks.


### Prerequisites

These playbooks are design to run on a Ubuntu Server 16.04 OS. Also, make sure to have a working Ansible installation.


### Installing

Start by cloning the repo, and populate the hosts file with your own servers, and provide the master server IP address in the [all:vars] section.

```
git clone https://github.com/antlamont/ansible-securityonion.git
```

Then, edit the setup configuration files in /roles/playbook/files/sosetup.conf to set up the ssh username you're going to use. You can also customize these files to enable/disable any options you want or do not want.

```
SSH_USERNAME=''
```

The last manual tweak to do is to set the log size limit in these same sosetup files

```
LOG_SIZE_LIMIT=124000000000
```

## Running the playbook

Belowe are the commands to run the playbooks. The first playbook is going to install everything needed to run the setup, but is not going to run the setup itself. The second one runs the setup.

### Master server

```
ansible-playbook -i hosts -l master master.yml -v -k --ask-become-pass
```

```
ansible-playbook -i hosts -l master so_setup.yml -v -k --ask-become-pass
```

### Storage nodes

```
ansible-playbook -i hosts -l storage_nodes storage_nodes.yml -v -k --ask-become-pass
```

```
ansible-playbook -i hosts -l storage_nodes so_setup.yml -v -k --ask-become-pass
```


### Forward nodes

```
ansible-playbook -i hosts -l forward_nodes forward_nodes.yml -v -k --ask-become-pass
```

```
ansible-playbook -i hosts -l forward_nodes so_setup.yml -v -k --ask-become-pass
```
