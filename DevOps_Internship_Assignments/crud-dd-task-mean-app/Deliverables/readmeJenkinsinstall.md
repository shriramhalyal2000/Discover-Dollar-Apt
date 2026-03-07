# Jenkins Installation on EC2 - Complete Guide

## Overview
This document provides detailed steps for installing Jenkins on an Amazon EC2 instance running Amazon Linux 2023.

## Prerequisites
- EC2 instance running Amazon Linux 2023
- SSH access to the EC2 instance
- PEM key file for authentication
- Security group configured to allow SSH (port 22) and Jenkins (port 8080)

## Installation Steps

### 1. Connect to EC2 Instance
bash
ssh -i "crud-dd-task.pem" ec2-user@ec2-98-86-161-181.compute-1.amazonaws.com


### 2. Copy Installation Script to EC2
bash
scp -i "crud-dd-task.pem" install-jenkins-ec2.sh ec2-user@ec2-98-86-161-181.compute-1.amazonaws.com:~/


### 3. Execute Installation Script
bash
ssh -i "crud-dd-task.pem" ec2-user@ec2-98-86-161-181.compute-1.amazonaws.com "chmod +x install-jenkins-ec2.sh && ./install-jenkins-ec2.sh"


## What the Installation Script Does

### System Updates
- Updates all system packages using `yum update -y`

### Java Installation
- Installs Java 11 Amazon Corretto (required for Jenkins)
- Command: `sudo yum install -y java-11-amazon-corretto`

### Jenkins Installation
- Downloads Jenkins repository configuration
- Imports Jenkins GPG key for package verification
- Installs Jenkins package
- Starts and enables Jenkins service

### Docker Installation
- Installs Docker for containerization support
- Starts and enables Docker service
- Adds jenkins and ec2-user to docker group for permissions

### Docker Compose Installation
- Downloads and installs latest Docker Compose
- Makes it executable and places in `/usr/local/bin/`

### Git Installation
- Installs Git for version control support

## Post-Installation

### Access Jenkins
- **URL**: `http://ec2-98-86-161-181.compute-1.amazonaws.com:8080`
- **Initial Admin Password**: `e4b4690b69c044b09b32119ba34448c6`

### Security Group Configuration
Ensure your EC2 security group has the following inbound rules:
- **SSH**: Port 22 (for administration)
- **Jenkins**: Port 8080 (for web access)

### First-Time Setup
1. Navigate to Jenkins URL in your browser
2. Enter the initial admin password when prompted
3. Install suggested plugins or select plugins manually
4. Create your first admin user
5. Configure Jenkins URL

## Verification Commands

### Check Jenkins Status
bash
sudo systemctl status jenkins


### Check Docker Status
bash
sudo systemctl status docker
```

### Verify Java Installation
bash
java -version


### Check Jenkins Logs
bash
sudo journalctl -u jenkins -f


## Troubleshooting

### Jenkins Not Starting
- Check if port 8080 is already in use: `sudo netstat -tlnp | grep :8080`
- Review Jenkins logs: `sudo journalctl -u jenkins`

### Permission Issues
- Ensure jenkins user is in docker group: `groups jenkins`
- Restart Jenkins after group changes: `sudo systemctl restart jenkins`

### Firewall Issues
- Check security group settings in AWS Console
- Verify local firewall: `sudo firewall-cmd --list-all` (if firewalld is running)

## Additional Configuration

### Change Jenkins Port (Optional)
1. Edit Jenkins configuration: `sudo vi /etc/sysconfig/jenkins`
2. Modify `JENKINS_PORT` variable
3. Restart Jenkins: `sudo systemctl restart jenkins`

### Enable HTTPS (Recommended for Production)
1. Generate SSL certificate
2. Configure reverse proxy (nginx/apache)
3. Update security group for HTTPS (port 443)

## Installed Components Summary
- **Jenkins**: Latest stable version (2.528.2)
- **Java**: Amazon Corretto 11
- **Docker**: Latest version with Docker Compose
- **Git**: For version control integration

## Support
For issues or questions, refer to:
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)