# Home Assistant Core Deployment Guide

This guide provides instructions for manually deploying Home Assistant Core from source.

## System Requirements

- Python 3.10 or later
- pip (Python package manager)
- Git
- System development tools

## Pre-installation Steps

1. Install system dependencies:
   ```bash
   sudo apt-get update
   sudo apt-get install -y \
       python3-pip \
       python3-dev \
       python3-venv \
       libffi-dev \
       libssl-dev \
       libjpeg-dev \
       zlib1g-dev \
       autoconf \
       build-essential \
       libopenjp2-7 \
       libtiff5 \
       libturbojpeg0-dev \
       tzdata
   ```

2. Clone the repository:
   ```bash
   git clone https://github.com/home-assistant/core.git
   cd core
   ```

## Installation Steps

1. Create and activate a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

2. Upgrade pip:
   ```bash
   pip3 install --upgrade pip
   ```

3. Install requirements:
   ```bash
   pip3 install wheel
   pip3 install -r requirements.txt
   ```

4. Install Home Assistant:
   ```bash
   pip3 install -e .
   ```

## Configuration

1. Create the configuration directory:
   ```bash
   mkdir ~/.homeassistant
   ```

2. Copy the default configuration:
   ```bash
   cp ./homeassistant/config/default_config.yaml ~/.homeassistant/configuration.yaml
   ```

## Running Home Assistant

1. Start Home Assistant:
   ```bash
   hass --config ~/.homeassistant
   ```

2. Access the web interface:
   - Open a web browser
   - Navigate to `http://localhost:8123`
   - Complete the initial setup process

## Common Issues and Troubleshooting

1. Dependency Conflicts:
   - If you encounter dependency conflicts, try installing dependencies one by one
   - Use `pip3 install --no-deps` for problematic packages
   - Consider using a specific version of Python (3.10 recommended)

2. Port Conflicts:
   - Ensure port 8123 is not in use
   - You can specify a different port using `hass --config ~/.homeassistant -p <port_number>`

3. Permission Issues:
   - Ensure proper permissions for the ~/.homeassistant directory
   - Run `chmod -R 755 ~/.homeassistant`

## Testing

1. Run the test suite:
   ```bash
   python3 -m pytest tests/
   ```

2. Test specific components:
   ```bash
   python3 -m pytest tests/components/<component_name>
   ```

## Notes

- Home Assistant requires significant system resources
- Some components may require additional system dependencies
- Regular backups of the configuration directory are recommended
- Monitor the home-assistant.log file for troubleshooting

## Additional Resources

- Official Documentation: https://www.home-assistant.io/docs/
- GitHub Repository: https://github.com/home-assistant/core
- Community Forums: https://community.home-assistant.io/