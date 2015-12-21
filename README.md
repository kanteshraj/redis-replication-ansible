# redis-replication-ansible

## Requirements

- Vagrant
- Ansible

## Usage

### Setup

Clone this repository.

    $ git clone https://github.com/kanteshraj/redis-replication-ansible.git
    $ cd redis-replication-ansible

### Execute

Start vagrant VMs and provision by using ansible.

    $ vagrant up

(After the first time) Execute ansible playbook.

    $ vagrant provision

Check replication status.

    $ vagrant ssh node2 --command "redis-cli info | grep ^role"
