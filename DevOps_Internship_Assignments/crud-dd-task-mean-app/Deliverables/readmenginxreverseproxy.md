# Nginx Reverse Proxy Setup Guide

## Overview
This guide documents the step-by-step process to set up Nginx as a reverse proxy on EC2 to route port 80 to the frontend application running on port 4200.

## Prerequisites
- EC2 instance running with Docker containers
- Frontend container running on port 4200
- Backend container running on port 8080
- SSH access to EC2 instance

## Step 1: Install Nginx

bash
# SSH into EC2 instance
ssh -i "crud-dd-task.pem" ec2-user@ec2-98-86-161-181.compute-1.amazonaws.com

# Update system and install Nginx
sudo yum update -y
sudo yum install -y nginx


## Step 2: Stop Nginx Service

bash
# Stop nginx to configure it
sudo systemctl stop nginx


## Step 3: Create Nginx Reverse Proxy Configuration

bash
# Remove any existing configurations
sudo rm -f /etc/nginx/conf.d/*

# Create the proxy configuration file
sudo sh -c 'printf "server {\n    listen 80;\n    location / {\n        proxy_pass http://localhost:4200;\n        proxy_set_header Host localhost:4200;\n        proxy_set_header X-Real-IP \$remote_addr;\n        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;\n    }\n}\n" > /etc/nginx/conf.d/proxy.conf'


## Step 4: Test and Start Nginx

bash
# Test nginx configuration
sudo nginx -t

# Start nginx service
sudo systemctl start nginx

# Enable nginx to start on boot
sudo systemctl enable nginx

## Step 5: Verify Setup

bash
# Test local access
curl http://localhost

# Check nginx status
sudo systemctl status nginx

# View configuration
sudo cat /etc/nginx/conf.d/proxy.conf


## Final Configuration File Content

**File:** `/etc/nginx/conf.d/proxy.conf`
nginx
server {
    listen 80;
    location / {
        proxy_pass http://localhost:4200;
        proxy_set_header Host localhost:4200;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}


## Security Group Configuration

Add inbound rule to EC2 Security Group:
- **Type:** HTTP
- **Port:** 80
- **Source:** 0.0.0.0/0

## Access URLs

- **Frontend Application:** http://54.236.201.80(port 80)
- **Direct Frontend Access:** http://54.236.201.80:4200
- **Backend API:** http://54.236.201.80:8080

## Container Status

```bash
# Check running containers
sudo docker ps


Expected containers:
- `frontend` - Port 4200:4200
- `backend` - Port 8080:8080  
- `mongo` - Internal only

## Troubleshooting

### Issue: "Invalid Host header"
**Solution:** Set Host header to `localhost:4200` in proxy configuration

### Issue: Nginx won't start
**Solution:** Check configuration syntax with `sudo nginx -t`

### Issue: 502 Bad Gateway
**Solution:** Ensure frontend container is running on port 4200

## Commands Summary

bash
# Install
sudo yum install -y nginx

# Configure
sudo sh -c 'printf "server {\n    listen 80;\n    location / {\n        proxy_pass http://localhost:4200;\n        proxy_set_header Host localhost:4200;\n        proxy_set_header X-Real-IP \$remote_addr;\n        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;\n    }\n}\n" > /etc/nginx/conf.d/proxy.conf'

# Start
sudo nginx -t && sudo systemctl start nginx && sudo systemctl enable nginx

# Test
curl http://localhost


## Result
 Application accessible via port 80: http://54.236.201.80