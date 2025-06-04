# Distcc Manual Deployment Guide

## Overview
Distcc is a program that distributes builds of C, C++, Objective C, or Objective C++ code across several machines on a network. This guide provides step-by-step instructions for deploying distcc.

## Prerequisites

### System Requirements
- Linux/Unix-based operating system
- GCC or compatible C/C++ compiler
- Python 3.x
- Network connectivity (for distributed compilation)

### Required Dependencies
```bash
# Core build dependencies
sudo apt-get install -y \
    autoconf \
    automake \
    python3-dev \
    libiberty-dev \
    python3-setuptools \
    libtool \
    make \
    gcc \
    g++ \
    pkg-config
```

## Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/distcc/distcc.git
   cd distcc
   ```

2. **Generate Build Files**
   ```bash
   ./autogen.sh
   ```

3. **Configure the Build**
   ```bash
   ./configure
   ```

4. **Compile the Source**
   ```bash
   make
   ```

5. **Install the Software**
   ```bash
   sudo make install
   ```

## Configuration

1. **Server Setup**
   - Create distcc user (optional but recommended):
     ```bash
     sudo useradd -r -s /bin/false distcc
     ```
   
   - Configure the distcc daemon:
     ```bash
     sudo distccd --daemon --allow 192.168.1.0/24 --log-file=/var/log/distccd.log
     ```
     Replace `192.168.1.0/24` with your network subnet.

2. **Client Setup**
   - Set environment variables:
     ```bash
     export DISTCC_HOSTS='localhost server1 server2'
     export MAKEFLAGS='-j8'  # Adjust based on available cores
     ```

   - Configure distcc masquerade (for automatic compiler redirection):
     ```bash
     mkdir -p /usr/lib/distcc
     cd /usr/lib/distcc
     ln -s /usr/bin/distcc gcc
     ln -s /usr/bin/distcc g++
     ln -s /usr/bin/distcc cc
     ln -s /usr/bin/distcc c++
     ```

## Testing

1. **Basic Functionality Test**
   ```bash
   distcc --version
   ```

2. **Network Configuration Test**
   ```bash
   distcc --show-hosts
   ```

3. **Compilation Test**
   ```bash
   # Create a test C file
   echo '#include <stdio.h>
   int main() {
       printf("Hello, World!\n");
       return 0;
   }' > test.c
   
   # Compile using distcc
   distcc gcc -o test test.c
   ```

## Troubleshooting

1. **Common Issues**
   - Check network connectivity between clients and servers
   - Verify firewall settings (default port is 3632)
   - Ensure consistent compiler versions across all machines
   - Check log files at `/var/log/distccd.log`

2. **Monitoring**
   - Use `distccmon-text` for text-based monitoring
   - Use `distccmon-gnome` for GUI monitoring (if installed)

## Security Considerations

1. **Network Security**
   - Use `--allow` option to restrict access to trusted networks
   - Consider using SSH tunneling for secure remote compilation
   - Keep distcc updated to the latest version

2. **File System Security**
   - Run distccd as non-root user
   - Implement appropriate file permissions
   - Use chroot if needed

## Performance Optimization

1. **Client-side Optimization**
   - Adjust `-j` parameter based on available cores
   - Configure DISTCC_HOSTS with appropriate load factors
   - Use compression for slower networks: `export DISTCC_COMPRESS=1`

2. **Server-side Optimization**
   - Monitor system resources
   - Adjust max jobs per client
   - Configure appropriate nice levels

## Maintenance

1. **Regular Tasks**
   - Monitor log files
   - Update distcc when new versions are available
   - Check for network connectivity issues
   - Verify compiler version consistency

2. **Backup Considerations**
   - Backup configuration files
   - Document network setup
   - Maintain list of connected clients/servers

## References
- [Official Distcc Documentation](https://github.com/distcc/distcc)
- [Distcc Man Page](https://linux.die.net/man/1/distcc)