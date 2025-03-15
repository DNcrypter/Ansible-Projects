# 🍁 Ansible playbook to setup 3 tier web application

## Introduction

This project provides an Ansible playbook to automate the setup of a web application on a Linux server. It installs essential packages like `Nginx`, `MySQL`, and `Python dependencies`, configures the web server, sets up a MySQL database, and includes monitoring using `htop`. The playbook ensures a smooth and consistent deployment for web applications, following best DevOps practices.

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
        [![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue)](https://www.linkedin.com/in/nikhil--chaudhari/)
        [![Medium](https://img.shields.io/badge/Medium-Writeups-black)](https://medium.com/@nikhil-c)


## 🍁Architecture

The architecture of this project consists of the following main components:

1. **Web Servers**: Target machines where the playbook will deploy the application. These machines will have Nginx and MySQL installed and configured, along with the web application repository.
2. **Nginx Web Server**: Acts as the reverse proxy and serves the web application.
3. **MySQL Database**: A relational database used for storing application data.
4. **System Monitoring**: Uses `htop` to monitor system performance, scheduled to run periodically via a cron job.
5. **Log Rotation**: Configured for Nginx logs to avoid filling up the disk with old log files.

The playbook is organized into a modular structure using Ansible **``roles``** to handle tasks, templates, files, and variables efficiently.

## Prerequisites

Before running the playbook, ensure you have the following:

- **Ansible 2.x or higher** installed on your control machine.
- **Linux-based servers** (preferably Ubuntu or Debian) to execute the playbook on.
- **MySQL server** access credentials for creating the database and user.
- SSH access to the web servers listed in your inventory file for passwordless authentication from ansible.
- **Git** installed on the web servers to clone the application repository.

### 🍁 Install Ansible

* If you don’t have Ansible installed, you can install it using the following commands:

```bash
# On Ubuntu/Debian
sudo apt update
sudo apt install ansible

# Or, using python pip
pip install ansible
```


## 🍁 Setup
* Clone the repository:
```bash
git clone  https://github.com/yourusername/ansible-devops-web-app.git
cd ansible-devops-web-app

```

### Modify Variables
Edit the roles/web-app-setup/vars/main.yml file to match your application's settings:

* **app_name**: Name of your web application.
* **app_repo**: The Git repository URL of your web application.
* **db_name**: Name of the database you want to create.
* **db_user**: Username for the database user.
* **db_password**: Password for the database user.


```yml
app_name: "sample-web-app"
app_repo: "https://github.com/username/sample-web-app.git"
app_dir: "/var/www/{{ app_name }}"
db_name: "sample_db"
db_user: "app_user"
db_password: "securepassword"

```

### Configure Inventory
Update the **`inventory`** file with the target web servers' IP addresses or domain names. Example:
```bash
[web_servers]
web1.example.com
web2.example.com

```
## 🍁 Installation
### Install Dependencies
If the system doesn't have some required tools, such as python3-pip, git, or htop, the playbook will automatically install them for you.

### Run the Playbook
Execute the Ansible playbook to set up the application:
```bash
ansible-playbook playbook.yml
```


 The playbook will perform the following steps on the web servers:

1. Install necessary packages: Nginx, MySQL, Python3, Git, htop, and logrotate.
2. Clone the web application repository from GitHub.
3. Configure Nginx to serve the application.
4. Set up MySQL, create the required database, and configure the user with proper permissions.
5. Set up log rotation for Nginx logs to ensure logs don’t consume too much disk space.
6. Deploy a system performance monitoring script (htop), which will run every 10 minutes via a cron job.

## 🍁 Implementation
### Tasks
* **Install Packages**: Ensures that all necessary software (Nginx, MySQL, Git, etc.) is installed.
* **Configure Nginx**: Creates a virtual host configuration to serve the application via Nginx, leveraging a Jinja2 template.
* **Database Setup**: Creates a MySQL database and user with specified privileges.
* **Log Rotation**: Copies a custom nginx_logrotate.conf to ensure that Nginx logs are rotated regularly.
* **System Monitoring**: Sets up a simple script that runs htop every 10 minutes to monitor system resources.

### Roles
* **web-app-setup**: This role includes tasks, templates, and files required to set up the web application.
* **Tasks**: The main actions to install packages, configure Nginx, set up the database, and more.
* **Templates**: Jinja2 templates for dynamic file configuration (e.g., Nginx).
* **Files**: Files like log rotation configuration.


### Handlers
* **Reload nginx:** Reloads Nginx when the configuration is updated or a new site is enabled.

## 🍁 Conclusion

This project provides an efficient and automated way to deploy a web application with a reliable stack consisting of **`Nginx`** and **`MySQL`**. It simplifies the process of setting up a web application by ensuring that all necessary components are installed and configured properly, including monitoring and log rotation. Using this playbook, you can achieve a consistent, repeatable deployment process for your web applications across multiple servers.

Feel free to modify and expand this setup to meet your specific needs. If you have any issues or need help, please open an issue in the GitHub repository.

