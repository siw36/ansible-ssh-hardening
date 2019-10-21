ansible-ssh-hardening
=========
![Ansible Role](https://img.shields.io/ansible/role/42253.svg?color=blue) ![Ansible Quality Score](https://img.shields.io/ansible/quality/42253.svg?color=blue) ![Ansible Role](https://img.shields.io/ansible/role/d/42253.svg?color=blue)

This role performs basic SSH hardening tasks, including:  
- Change the SSH port
- Disable SSH password authentication
- Set SELinux settings
- Allow the new SSH port in firewalld
- Install and configure fail2ban for SSH

Get this role
------------
```bash
ansible-galaxy install --roles-path ./roles/ siw36.ansible_ssh_hardening
```

Requirements
------------

- RHEL based OS
- The user used on the remote host must have permissions to execute `sudo` commands without being prompted for password confirmation.

Role Variables
--------------

| Name | Description | Default value |
|---|---|---|
| sshPort | New SSH port | 1337 |
| f2bEnabled | Enable fail2ban for SSH | true |
| f2bRetries | Amount of allowed failed logins before banning | 5 |
| f2bBanTime | Ban time in seconds | 3600 |
| f2bIgnoreIP | List of ignored IPs/Subnets | 127.0.0.1/32 |
| vmAdmins | List of user accounts and public SSH keys that should get access to the machine | <none - optional> |
| allowedInterfaces | List of network interfaces on which the SSHD service should be available | <none - optional> |


Example Playbook
----------------

playbook.yml  
```yaml
- hosts: servers
  become: true
  roles:
     - siw36.ansible_ssh_hardening
```

vars/main.yml
```yaml
vmAdmins:
  - user: siw36
    sshKey: ssh-rsa xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx siw36
allowedInterfaces:
  - eth0

```

License
-------

GNU General Public License v3.0

Author Information
------------------

Created by Robin 'siw36' Klussmann (07/2019)
