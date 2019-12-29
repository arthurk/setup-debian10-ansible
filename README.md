Ansible playbook for initial setup of debian10 server.

It will:

- create sudo group (wheel)
- create user (in wheel group) and copy local ssh key
- ssh: disable password based logins, disable root login
- install mosh, ufw, fail2ban, htop, tmux, docker, docker-compose
- install unattended-upgrades and enable automatic security upgrades

Usage:

```sh
# create server (example hetzner)
hcloud server create --name myserver --image debian-10 --type cx11 --ssh-key 123

# update ansible inventory
# /etc/ansible/hosts

    [servers]
    myserver ansible_host=<server_ip>

    [servers:vars]
    ansible_python_interpreter=/usr/bin/python3

# make sure it can connect
ansible all -m ping -u root

# first time must be ron as root to create user
ansible-playbook playbook.yml -l myserver -u root

# next runs can be done as user
ansible-playbook playbook.yml -l myserver -u arthur

# login to server
mosh arthur@<server_ip>
```
