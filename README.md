# Ansible Playbook for User Creation on Cloud Servers

## Overview
This Ansible playbook is designed to automate the process of creating a new user with sudo privileges on cloud servers. It handles the following tasks:
- Identifying a sudo group from the server's sudoers file.
- Creating a new user and adding them to the identified sudo group.
- Setting a password for the new user.
- Enabling password authentication in SSH.

## Prerequisites
- Ansible installed on the control machine.
- SSH access to the target cloud servers.
- Sudo privileges on the target servers.

## Files Description
1. **`create_user.yaml`**: The main playbook file.
2. **`vars.yaml`**: A variables file containing user details.
3. **`hosts.ini`**: An inventory file listing the cloud servers.

## Configuration

### Setting Up Variables
Edit the `vars.yaml` file to set the username and password for the new user:
```yaml
---
user_name: [desired_username]
user_password: [desired_password]
```
Replace `[desired_username]` and `[desired_password]` with your desired username and password.

### Configuring the Inventory
Update the `hosts.ini` file with your cloud server details:
```
[cloud_servers]
[ip_address] ansible_user=[remote_username] ansible_ssh_private_key_file=[path_to_private_key]
```
Replace `[ip_address]`, `[remote_username]`, and `[path_to_private_key]` with your server's IP address, remote username, and path to the SSH private key file, respectively.

## Running the Playbook
To run the playbook, use the following command:
```bash
ansible-playbook -i hosts.ini create_user.yaml
```

## Notes
- Ensure that the user running this playbook has sufficient privileges on the control machine and the target servers.
- The playbook checks for a sudo group in the target's sudoers file. If no group is found, it will fail with an appropriate message.
- Password for the new user is hashed using SHA-512 algorithm for security.

---

This README provides a comprehensive guide to your Ansible setup, ensuring that anyone with basic Ansible knowledge can understand and use your playbook.