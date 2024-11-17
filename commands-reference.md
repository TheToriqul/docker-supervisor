# Docker Supervisor Command Reference Guide

## Table of Contents
- [Container Management](#container-management)
- [Process Control](#process-control)
- [Monitoring Commands](#monitoring-commands)
- [Troubleshooting](#troubleshooting)
- [Configuration Management](#configuration-management)

> **Author**: Md Toriqul Islam  
> **Description**: Reference guide for Docker Supervisor commands and operations  
> **Learning Focus**: Container process management and monitoring  
> **Note**: This is a reference guide. Do not execute commands directly without understanding their implications.

## Container Management

### Building the Container
```bash
# Build the LAMP stack image
docker build -t lamp-supervisor .

# Build with no cache (for fresh builds)
docker build --no-cache -t lamp-supervisor .
```

### Container Operations
```bash
# Start the container
docker run -d \
    -p 80:80 \
    -p 3306:3306 \
    --name lamp-container \
    lamp-supervisor

# Stop the container
docker stop lamp-container

# Remove the container
docker rm lamp-container

# Restart the container
docker restart lamp-container
```

## Process Control

### Supervisor Management
```bash
# Access supervisor control
docker exec -it lamp-container supervisorctl

# Check process status
docker exec lamp-container supervisorctl status

# Restart specific process
docker exec lamp-container supervisorctl restart apache2

# Stop specific process
docker exec lamp-container supervisorctl stop mysql

# Start specific process
docker exec lamp-container supervisorctl start apache2
```

## Monitoring Commands

### Container Monitoring
```bash
# View container logs
docker logs lamp-container

# Follow container logs
docker logs -f lamp-container

# View process list
docker top lamp-container

# Container resource usage
docker stats lamp-container
```

### Process Monitoring
```bash
# Check running processes
docker exec lamp-container ps aux

# View supervisor logs
docker exec lamp-container cat /var/log/supervisor/supervisord.log

# Monitor Apache logs
docker exec lamp-container tail -f /var/log/apache2/error.log

# Monitor MySQL logs
docker exec lamp-container tail -f /var/log/mysql/error.log
```

## Troubleshooting

### Debug Commands
```bash
# Check container health
docker inspect lamp-container

# Enter container shell
docker exec -it lamp-container bash

# Check network connectivity
docker exec lamp-container netstat -tulpn

# View supervisor configuration
docker exec lamp-container cat /etc/supervisor/conf.d/supervisord.conf
```

## Configuration Management

### Apache Configuration
```bash
# Edit Apache configuration
docker exec -it lamp-container vim /etc/apache2/apache2.conf

# Restart Apache
docker exec lamp-container supervisorctl restart apache2
```

### MySQL Configuration
```bash
# Access MySQL
docker exec -it lamp-container mysql -u root -p

# Edit MySQL configuration
docker exec -it lamp-container vim /etc/mysql/my.cnf

# Restart MySQL
docker exec lamp-container supervisorctl restart mysql
```

## Learning Notes

1. Supervisor manages multiple processes within a single container
2. Process monitoring ensures high availability
3. Centralized logging simplifies debugging
4. Custom restart policies enhance reliability
5. Container resource management is crucial

> 💡 **Best Practice**: Always check process status after configuration changes

> ⚠️ **Warning**: Stopping critical processes may affect container stability

> 📝 **Note**: Keep supervisor configuration up-to-date with process changes