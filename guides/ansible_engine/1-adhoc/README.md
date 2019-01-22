# Exercise - Running Ad-hoc commands

For our first exercise, we are going to run some ad-hoc commands to help you get a feel for how Ansible works.  Ansible Ad-Hoc commands enable you to perform tasks on remote nodes without having to write a playbook.  They are very useful when you simply need to do one or two things quickly and often, to many remote nodes.

## Section 1: Definition of the inventory

Inventories are crucial to Ansible as they define remote machines on which you wish to run commands or your playbook(s). In this lab the inventory is provided by your instructor. The inventory is an ini formatted file listing your hosts, sorted in groups, additionally providing some variables. It looks like:

```bash
[all:vars]
ansible_user=rwolters
ansible_ssh_pass=averysecretpassword
ansible_port=22

[web]
node-ansible_host=.22.33.44
node-2 ansible_host=22.33.44.55
node-3 ansible_host=33.44.55.66

[control]
ansible ansible_host=44.55.66.77
```

Your individual inventory is already present in your lab environment underneath `lightbulb/lessons/lab_inventory/$USERNAME-instances.txt`, where `$USERNAME` is replaced by your individual username.

## Section 2: Basic Ansible configuration

Ansible needs to know which inventory file should be used. By default it checks for the inventory file at `/etc/ansible/hosts`. You need to point Ansible to your own, lab specific inventory file. One way to do this is to specify the path to the inventory file with the `-i` option to the ansible command:

```bash
ansible -i hosts ...
```

To avoid the need to specify the inventory file each time, the inventory can also be configured in the configuration file `.ansible.cfg`. If this file is present, Ansible will read configuration parameters like the inventory location and others from this file.

On your control node, such a file is already present right in the home directory of your user. It is already customized to point to your inventory file, so there is nothing further you have to do.

## Section 3: Ping a host

Let's start with something basic and use the `ping` module to test that Ansible has been installed and configured correctly and all hosts in your inventory are responsive.

```bash
ansible all -m ping
```

## Section 4: Run a typical command

Now let's see how we can run a typical Linux shell command and format the output using the `command` module.

```bash
ansible web -m command -a "uptime" -o
```

## Section 5: Gather facts about target node

We can use an ad-hoc command with the `setup` module to display the many facts Ansible can discover about each node in its inventory.

```bash
ansible all -m setup
```

## Section 6: Install package

Now, let's install Apache using the `yum` module.

```bash
ansible web -m yum -a "name=httpd state=present" -b
```

Usually, only root users are allowed to install packages. So this is a case where we need privilege escalation and a sudo that has to be setup properly. We need to instruct ansible to use sudo to run the command as root by using the parameter `-b` (think "become").

## Section 7: Start service

OK, Apache is installed now so let's start it up using the `service` module.

```bash
ansible web -m service -a "name=httpd state=started" -b
```

## Section 8: Stop service

Finally, let's clean up after ourselves.  First, stop the httpd service.

```bash
ansible web -m service -a "name=httpd state=stopped" -b
```

## Section 9: Remove package

Next, remove the Apache package.

```bash
ansible web -m yum -a "name=httpd state=absent" -b
```

---
**NOTE:** Additional `ansible` options

The way `ansible` works can be influenced by various options which can be listed via `ansible --help`:

```bash
ansible --help
Usage: ansible <host-pattern> [options]

Define and run a single task 'playbook' against a set of hosts

Options:
  -a MODULE_ARGS, --args=MODULE_ARGS
                        module arguments
  --ask-vault-pass      ask for vault password
  -B SECONDS, --background=SECONDS
                        run asynchronously, failing after X seconds
                        (default=N/A)
  -C, --check           don't make any changes; instead, try to predict some
                        of the changes that may occur
  -D, --diff            when changing (small) files and templates, show the
                        differences in those files; works great with --check
[...]
```

---

[Click Here to return to the Ansible Lightbulb - Ansible Engine Guide](../README.md)
