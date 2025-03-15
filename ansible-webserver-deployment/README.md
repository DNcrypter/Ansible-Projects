# 🍁Ansible Apache Server Deployment Project



[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
        [![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
        [![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)



## Table of Contents

- [Introduction](#introduction)
- [Requirements](#Requirements )
- [Setup](#setup)
- [Directory Structure](#Directory Structure)
- [Upcomming Modification](#Future upcomming Improvements)


## Introduction

This repository contains an **Ansible-based** project for deploying and managing web servers. The project leverages **Ansible** to configure Apache HTTP servers and deploy website files to multiple web servers in a production environment.

The project follows best practices for organizing Ansible playbooks, roles, and inventory files to ensure scalability and ease of maintenance.


## Requirements
 To get started with this project, you will need the following tools installed:
- [Ansible](https://www.ansible.com/) - For configuration management.
- A Unix-based environment (Linux/macOS).
- SSH access to the target servers for Ansible to configure them.

## setup
### 1. Install Ansible
Make sure **Ansible** is installed:
```bash
sudo apt-get update
sudo apt-get install ansible
```
### 2. Inventory Configuration
The inventory/production.ini file contains a list of your target servers. For example:
```
[web_servers]
webserver1 ansible_host=192.168.1.10
webserver2 ansible_host=192.168.1.11
```
Update the IP addresses of your actual servers accordingly.

### 3. Configure Variables
You can set common variables in group_vars/all.yml. For example:
```
website_root: /var/www/html
website_source_dir: /home/ubuntu/website_files
apache_version: "2.4"
```
For host-specific variables, create individual files in the host_vars/ directory.

### 4. Run Ansible Playbooks
You can deploy the Apache web server and website using the following command:
```
ansible-playbook -i inventory/production.ini playbooks/deploy_apache.yml

```
**This will:**

* Install Apache HTTP server.
* Deploy your website files.
* Configure the firewall to allow HTTP traffic on port 80.
* Start and enable Apache to run on boot.

## Directory Structure :
* **`playbooks/`**: Contains the main Ansible playbooks, such as deploy_apache.yml which installs and configures Apache and deploys website files.
* **`roles/`**: Organized into roles like apache and website for easier management and reuse of tasks.
* **`inventory/`**: Contains the list of hosts and their corresponding configuration.
* **`group_vars/`**: Defines shared variables for all hosts in the group.
* **`host_vars/`**: Defines variables specific to individual hosts.


## Future upcomming Improvements
* Adding SSL support and configure Apache with HTTPS.
* Integrate load balancing for high availability.
* Implement monitoring and logging solutions.
* Use Ansible Vault for securely storing sensitive data like passwords.


## Contributing
* Fork this repository.
* Create a new branch for your feature or fix.
* Make changes and commit them.
* Submit a pull request.

Let me know if you want to customize this further!
