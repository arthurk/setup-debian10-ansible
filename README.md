Ansible playbook for initial setup of debian10 server.

It will:

- create sudo group (wheel)
- create user (in wheel group) and copy local ssh key
- ssh: disable password based logins, disable root login
- install mosh
- install ufw, fail2ban
- install docker, docker-compose
- install tmux with custom config (see template dir)

Usage:

```
# create server (example hetzner)
hcloud server create --name myserver --image debian-10 --type cx11 --ssh-key 123

# first time must be ron as root to create user
ansible-playbook playbook.yml -l myserver -u root

# next runs can be done as user
ansible-playbook playbook.yml -l myserver -u arthur

# login to server
mosh arthur@<server_ip>
```
