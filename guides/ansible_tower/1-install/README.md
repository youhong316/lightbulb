# Exercise 1 - Installing Ansible Tower

In this exercise, we are going to get Ansible Tower installed on your control node

## Installing Ansible Tower

### Step 1

On your control node, change directories to /tmp

```bash
cd /tmp
```

### Step 2

Download the latest Ansible Tower package

```bash
curl -O http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-latest.tar.gz
```

### Step 3

Untar and unzip the package file

```bash
tar xvfz /tmp/ansible-tower-setup-latest.tar.gz
```

### Step 4

Change directories into the ansible tower package

```bash
cd /tmp/ansible-tower-setup-*/
```

### Step 5

Using an editor of your choice, open the inventory file

```bash
vi inventory
```

### Step 6

Fill a few variables out in an inventory file: `admin_password, pg_password, rabbitmq_password`

```ini
[tower]
localhost ansible_connection=local

[database]

[all:vars]
admin_password=*'ansibleWS'*

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password=*'ansibleWS'*

rabbitmq_port=5672
rabbitmq_vhost=tower
rabbitmq_username=tower
rabbitmq_password=*'ansibleWS'*
rabbitmq_cookie=cookiemonster

= Needs to be true for fqdns and ip addresses
rabbitmq_use_long_name=false
```

### Step 7

Run the Ansible Tower setup script

```bash
sudo ./setup.sh
```

---
**NOTE:** Installation will take some time
Step 7 will take approx. 10-15 minutes to complete.  This may be a good time to take a break.

---

### End Result

At this point, your Ansible Tower installation should be complete. You can access your Tower at the IP of the control node:

```bash
http://<IP_of_control_node>
```

### Ensuring Installation Success

You know you were successful if you are able to browse to your Ansible Tower's url (_control node's IP address_) and get something like this

![Ansible Tower Login Screen](ansible-lab-figure01-logon-screen.png)

---

[Click Here to return to the Ansible Lightbulb - Ansible Tower Guide](../README.md)
