# X-AnyLabeling Manual Deployment Guide

This document outlines the manual deployment process for X-AnyLabeling, including requirements, installation steps, and potential issues encountered.

## System Requirements

1. Operating System:
   - Linux (Ubuntu/Debian)
   - Windows
   - macOS

2. System Dependencies:
   - Python 3.7 or higher
   - Qt5 development tools
   - OpenCV
   - pip package manager

## Installation Steps

### 1. System Dependencies Installation

#### For Ubuntu/Debian:
```bash
sudo apt-get update
sudo apt-get install -y python3-pip python3-venv python3-dev python3-opencv
sudo apt-get install -y qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools
```

#### For Windows:
- Install Python 3.7+ from python.org
- Install Visual Studio Build Tools
- Qt5 will be installed via pip dependencies

#### For macOS:
```bash
brew install python3 qt@5 opencv
```

### 2. Python Virtual Environment Setup
```bash
python3 -m venv venv
source venv/bin/activate  # On Linux/macOS
# or
.\venv\Scripts\activate  # On Windows
```

### 3. X-AnyLabeling Installation

#### Method 1: Using pip
```bash
pip install x-anylabeling
```

#### Method 2: From Source
```bash
git clone https://github.com/CVHub520/X-AnyLabeling.git
cd X-AnyLabeling
pip install -r requirements.txt
python setup.py install
```

### 4. GPU Support (Optional)
For GPU support, install additional requirements:
```bash
pip install -r requirements-gpu.txt
```

## Known Issues and Solutions

1. Qt5 Installation Issues:
   - On Ubuntu: If qt5-default is not available, install individual Qt5 packages
   - On Windows: Ensure Visual Studio Build Tools are installed
   - On macOS: Use brew to install Qt5

2. OpenCV Dependencies:
   - Ensure system-level OpenCV is installed
   - Some features may require additional OpenCV contributions

3. CUDA Support:
   - For GPU acceleration, ensure CUDA toolkit and cuDNN are installed
   - Install appropriate versions matching your PyTorch installation

## Running the Application

1. From command line:
```bash
x-anylabeling
```

2. From source:
```bash
python -m anylabeling
```

## Testing

To verify the installation:

1. Basic functionality test:
```bash
x-anylabeling --version
```

2. Run unit tests:
```bash
pip install pytest
pytest tests/
```

## Troubleshooting

1. If encountering Qt-related errors:
   - Verify Qt5 installation
   - Check if PyQt5 is properly installed
   - Ensure no conflicts with other Qt versions

2. If encountering OpenCV errors:
   - Verify OpenCV installation
   - Check Python bindings are properly installed

3. For GPU-related issues:
   - Verify CUDA installation
   - Check GPU compatibility
   - Ensure matching CUDA toolkit and PyTorch versions

## Support

For additional support:
- GitHub Issues: https://github.com/CVHub520/X-AnyLabeling/issues
- Documentation: Refer to the docs directory in the repository