# lunchbox

Project Lunchbox is a resource for deploying Red Hat technologies on a single server that literally fits in a lunchbox.

Harware info: https://www.supermicro.com/manuals/superserver/mini-itx/MNL-2094.pdf

## Prerequisites

You need to configure an ansible host to execute these playbooks
- Ansible >= 2.6
- Git
- pip and pipenv
- screen or tmux (optional and your preference)

## Clone and configure the repository

1. Clone the lunchbox repository
```
$ git clone https://github.com/RedHatGov/lunchbox.git
```
2. Setup your vars file
```
$ cd lunchbox/
$ cp vars/vars.example.yml vars/vars.yml
$ vi vars/vars.yml
```
> NOTE: The vars example file only exposes the variables you must care about. If you need to dig deeper you'll have to dig into the roles.

3. Install the required roles from Ansible Galaxy
```
$ ansible-galaxy install -r playbooks/requirements.yml
```

## Configure pipenv

1. Install pipenv
```
$ pip install pipenv --user
```

2. Initialize the pipenv project
```
$ cd lunchbox/
$ pipenv --python 3.7
$ pipenv install
```

## To deploy the initial RHEL+KVM admin host

1. Follow the [instructions to create a bootable custom ISO](https://github.com/RedHatGov/hattrick/tree/master/admin-iso)
to install the base operating system for what will become the initial RHEL+KVM utility server
2. Verify your networking is the way you expect. We recommend one bridge for the LAN network (192.0.2.0/24) named br1
3. Run the kvm playbook from the lunchbox directory
```
$ ansible-playbook -i inventory/inventory.yml -e @vars/vars.yml playbooks/lunchbox/kvm.yml
```
