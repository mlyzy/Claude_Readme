# SABnzbd Installation and Testing Guide

## Overview
SABnzbd is an Open Source Binary Newsreader written in Python. This document outlines the installation and testing process for SABnzbd on Ubuntu Linux.

## System Requirements
- Python 3.x
- pip3
- Various system dependencies

## Installation Steps

### 1. System Dependencies
Install required system packages:
```bash
sudo apt-get update
sudo apt-get install -y python3 python3-pip python3-dev build-essential libffi-dev libssl-dev unrar p7zip-full par2
```

### 2. Clone Repository
```bash
git clone https://github.com/sabnzbd/sabnzbd.git
cd sabnzbd
```

### 3. Python Dependencies
Install Python requirements:
```bash
pip3 install -r requirements.txt
```

### 4. Running SABnzbd
To start SABnzbd:
```bash
python3 SABnzbd.py
```

By default, SABnzbd will run on http://localhost:8080

## Configuration Requirements

To use SABnzbd, you will need:
1. A Usenet provider account
2. NZB files or an indexer service
3. Proper configuration of download directories

## First-Time Setup
1. Access the web interface at http://localhost:8080
2. Follow the setup wizard to configure:
   - Download directories
   - Usenet server details
   - Basic preferences

## Manual Deployment Steps
If automatic installation fails, follow these steps:

1. Ensure all system dependencies are installed:
   ```bash
   sudo apt-get install python3 python3-pip python3-dev build-essential
   sudo apt-get install libffi-dev libssl-dev
   sudo apt-get install unrar p7zip-full par2
   ```

2. Create necessary directories:
   ```bash
   mkdir -p ~/Downloads/complete
   mkdir -p ~/Downloads/incomplete
   ```

3. Install Python dependencies manually if needed:
   ```bash
   pip3 install --user apprise sabctools feedparser configobj cheroot
   pip3 install --user cherrypy cryptography ujson
   ```

4. Configure permissions:
   ```bash
   chmod +x SABnzbd.py
   ```

5. Create a configuration file if needed:
   ```bash
   mkdir -p ~/.sabnzbd
   touch ~/.sabnzbd/sabnzbd.ini
   ```

## Testing
1. Start SABnzbd in console mode for testing:
   ```bash
   python3 SABnzbd.py -s localhost:8080 -b 0
   ```

2. Access the web interface at http://localhost:8080

3. Test basic functionality:
   - Configure a Usenet server
   - Add an NZB file
   - Monitor download progress
   - Verify completed downloads

## Common Issues
1. Port 8080 already in use
   - Solution: Use a different port with `-s localhost:xxxx`

2. Permission issues
   - Solution: Check directory permissions
   - Ensure write access to download directories

3. Missing dependencies
   - Solution: Check Python error messages
   - Install missing packages manually

## Note
This installation guide assumes a basic Ubuntu Linux environment. Additional steps may be required for other distributions or specific configurations.