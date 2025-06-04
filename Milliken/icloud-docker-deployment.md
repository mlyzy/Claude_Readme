# iCloud Docker Deployment Guide

## Prerequisites
1. A Linux system with Docker and Docker Compose installed
2. iCloud account credentials
3. Two-factor authentication enabled on your iCloud account
4. Sufficient disk space for your iCloud files

## Manual Deployment Steps

### 1. System Preparation
```bash
# Install Docker and Docker Compose
sudo apt-get update
sudo apt-get install -y docker.io docker-compose

# Start Docker service
sudo systemctl enable docker
sudo systemctl start docker

# Add your user to docker group (optional, for running docker without sudo)
sudo usermod -aG docker $USER
```

### 2. Project Setup
```bash
# Create project directory structure
mkdir -p ~/icloud-docker/{config,icloud}
cd ~/icloud-docker

# Create configuration file
# Create config/config.yaml with your iCloud settings
```

### 3. Configuration Files

#### config.yaml
Create this file in the config directory with the following structure:
```yaml
app:
  logger:
    level: "info"
    filename: "/config/icloud.log"
  credentials:
    username: "your-icloud-email@icloud.com"
    retry_login_interval: 600
  root: "/icloud"
drive:
  destination: "drive"
  remove_obsolete: false
  sync_interval: 300
photos:
  destination: "photos"
  remove_obsolete: false
  sync_interval: 500
  all_albums: false
```

#### docker-compose.yml
Create this file in your project root:
```yaml
version: '3'
services:
  icloud:
    image: mandarons/icloud-drive
    environment:
      - PUID=1000
      - PGID=1000
    env_file:
      - .env.icloud
    container_name: icloud
    restart: unless-stopped
    volumes:
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
      - ./icloud:/icloud
      - ./config:/config
```

#### .env.icloud
Create this file in your project root:
```
ENV_CONFIG_FILE_PATH=/config/config.yaml
```

### 4. Container Deployment
```bash
# Start the container
docker-compose up -d

# Authenticate with iCloud (required after container creation)
docker exec -it --user=abc icloud /bin/sh -c "icloud --username=<your-icloud-username> --session-directory=/config/session_data"
```

### 5. Authentication Process
1. When running the authentication command, you'll be prompted for your iCloud password
2. If 2FA is enabled, you'll receive a code on your trusted devices
3. Enter the 2FA code when prompted
4. The authentication session will be saved

### 6. Monitoring
- Check container logs:
```bash
docker logs icloud
```
- Monitor the icloud directory for downloaded files
- Check the config/icloud.log file for detailed logs

## Important Notes
1. The application only downloads files from iCloud; it does not upload local files to iCloud
2. Syncing can take longer depending on the number of files in your iCloud drive and photos
3. Make sure you have sufficient disk space for your iCloud content
4. The sync interval can be adjusted in the config.yaml file
5. For China server users, add `--region=china` to the authentication command

## Troubleshooting
1. If authentication fails, check your credentials and try again
2. If 2FA code is not received, ensure your trusted devices are accessible
3. Check logs for detailed error messages
4. Ensure Docker service is running
5. Verify correct file permissions on the config and icloud directories