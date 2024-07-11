# 🌐 Hosting a WordPress Website on AWS EC2 Instance

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Setting up the EC2 Instance](#setting-up-the-ec2-instance)
4. [Installing WordPress](#installing-wordpress)
5. [Configuring WordPress](#configuring-wordpress)
6. [Pushing to GitHub](#pushing-to-github)
7. [Best Practices for GitHub Projects](#best-practices-for-github-projects)

## Introduction
This guide provides a step-by-step process to host a WordPress website on an AWS EC2 instance and push the project to GitHub. By following these instructions, you will be able to set up a fully functional WordPress site and manage your code versioning through GitHub.

## Requirements
Before starting, ensure you have the following:
- An AWS account
- SSH access to the EC2 instance
- Basic knowledge of command-line interface (CLI)
- A GitHub account
- Git installed on your local machine

## Setting up the EC2 Instance

### 1. Launching an EC2 Instance
1. Log in to your AWS Management Console.
2. Navigate to the EC2 Dashboard and click on 'Launch Instance'.
3. Choose an Amazon Machine Image (AMI). For this guide, we will use the **Amazon Linux 2 AMI**.
4. Select an instance type. The **t2.micro** instance is suitable for this tutorial as it falls under the AWS Free Tier.
5. Configure the instance and add necessary storage (default is fine).
6. Add tags (optional).
7. Configure the security group. Allow **HTTP (port 80)** and **SSH (port 22)**.
8. Review and launch the instance. Download the key pair (.pem file) for SSH access.

### 2. Connecting to Your Instance
1. Open your terminal.
2. Change directory to where your key pair file is located.
3. Modify the permissions of the key pair file:
   ```bash
   chmod 400 your-key-pair.pem
   ```
4. Connect to your instance using SSH:
   ```bash
   ssh -i "your-key-pair.pem" ec2-user@your-ec2-public-ip
   ```

## Installing WordPress

### 1. Update Your Package Repository
```bash
sudo yum update -y
```

### 2. Install Apache Web Server
```bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

### 3. Install PHP
```bash
sudo yum install -y php php-mysqlnd
```

### 4. Install MySQL (MariaDB)
```bash
sudo yum install -y mariadb-server mariadb
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

### 5. Secure MySQL Installation
```bash
sudo mysql_secure_installation
```
Follow the prompts to set a root password and secure your installation.

### 6. Create a MySQL Database for WordPress
```bash
sudo mysql -u root -p
```
Within the MySQL shell, execute the following commands:
```sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 7. Download and Configure WordPress
1. Navigate to the Apache root directory:
   ```bash
   cd /var/www/html
   ```
2. Download the latest version of WordPress:
   ```bash
   sudo wget https://wordpress.org/latest.tar.gz
   sudo tar -xzf latest.tar.gz
   sudo mv wordpress/* .
   sudo rm -rf wordpress latest.tar.gz
   ```
3. Set the correct permissions:
   ```bash
   sudo chown -R apache:apache /var/www/html
   sudo chmod -R 755 /var/www/html
   ```

### 8. Configure WordPress to Connect to Your Database
1. Rename the sample configuration file:
   ```bash
   sudo mv wp-config-sample.php wp-config.php
   ```
2. Edit `wp-config.php` and update the database information:
   ```php
   define('DB_NAME', 'wordpress');
   define('DB_USER', 'wpuser');
   define('DB_PASSWORD', 'your_password');
   define('DB_HOST', 'localhost');
   ```

### 9. Finalise the WordPress Installation
1. Open your browser and navigate to your EC2 instance's public IP.
2. Follow the WordPress setup wizard to complete the installation.


