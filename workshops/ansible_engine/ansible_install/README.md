# Workshop: Installing Ansible

## Topics Covered

* Installing Ansible using pip or yum
* Configuration file basics

## What You Will Learn

* How easy it is to install and configure Ansible for yourself.

## The Assignment

1. Use pip to install the `ansible` package and its dependencies to you control machine.
1. Display the Ansible version and man page to STDOUT.
1. In `~/.ansible.cfg` file (create the file if it doesn't exist already) do the following:
  * Create a new directory `~/.ansible/retry-files` and set `retry_files_save_path` to it.
  * Set the Ansible system `forks` to 10

## Reference

* [Ansible Installation](http://docs.ansible.com/ansible/intro_installation.html)
* [Ansible Configuration File](http://docs.ansible.com/ansible/intro_configuration.html)

---

[Click Here to return to the Ansible Lightbulb - Ansible Engine Workshop](../README.md)
