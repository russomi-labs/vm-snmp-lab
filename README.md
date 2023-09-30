# ansible-vm-lab

A repo to get up and running with Ansible.

- [Getting Started](#getting-started)
  - [Create `.env` file](#create-env-file)
  - [Configure VMs](#configure-vms)
  - [Starting and Stopping the VM](#starting-and-stopping-the-vm)
  - [Downloading dependencies](#downloading-dependencies)
  - [Testing inventory with ad-hoc commands](#testing-inventory-with-ad-hoc-commands)
  - [Running the Ansible Playbook](#running-the-ansible-playbook)
- [Sample directory layout](#sample-directory-layout)
- [Resources](#resources)

## Getting Started

### Create `.env` file

1. Copy  `.env.example` as `.env`
2. Add/Update environment variables as needed
3. `source .env` to load variables into the current session

### Configure VMs

Update [Vagrantfile.yml](Vagrantfile.yml) to configure the VMs that will be created.

### Starting and Stopping the VM

```bash
# bring the VM up
vagrant up

# connect via ssh
vagrant ssh vagrant01

# stop the vm
vagrant halt

# delete the vm
vagrant destroy
```

### Downloading dependencies

Download the role and collection dependencies:

```bash
cd roles
ansible-galaxy install --roles-path . -r requirements.yml
ansible-galaxy collection install -r requirements.yml
```

### Testing inventory with ad-hoc commands

```bash
ansible test -a "date"
```

### Running the Ansible Playbook

To execute the playbook to configure the VM execute the following:

```bash
# run the playbook against a specific vm
ansible-playbook playbook.yml --limit vagrant01
```

## Sample directory layout

```bash
production                # inventory file for production servers
staging                   # inventory file for staging environment

group_vars/
   group1.yml             # here we assign variables to particular groups
   group2.yml
host_vars/
   hostname1.yml          # here we assign variables to particular systems
   hostname2.yml

library/                  # if any custom modules, put them here (optional)
module_utils/             # if any custom module_utils to support modules, put them here (optional)
filter_plugins/           # if any custom filter plugins, put them here (optional)

site.yml                  # main playbook
webservers.yml            # playbook for webserver tier
dbservers.yml             # playbook for dbserver tier
tasks/                    # task files included from playbooks
    webservers-extra.yml  # <-- avoids confusing playbook with task files
```

## Resources

- [Ansible User Guide](https://docs.ansible.com/ansible/2.8/user_guide/index.html)
- [Introduction to Ansible for Linux System Roles](https://linux-system-roles.github.io/documentation/intro-to-ansible-for-system-roles.html)
- [linux-system-roles](https://github.com/linux-system-roles)
- [Vagrant Advanced Examples](https://ctrlnotes.com/vagrant-advanced-examples/#-insert-custom-ssh-public-key-to-the-vm)
- [Ansible tips and tricks | Sample Ansible setup | Sample directory layout](https://docs.ansible.com/ansible/latest/tips_tricks/sample_setup.html#id1)
- [Red Hat Enterprise Linux (RHEL) System Roles](https://access.redhat.com/articles/3050101)
- [Ways to check for open ports on RHEL](https://access.redhat.com/discussions/3539801)
