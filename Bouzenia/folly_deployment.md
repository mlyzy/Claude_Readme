# Facebook Folly Library Deployment Guide

## Prerequisites

Before building and installing Folly, ensure you have the following dependencies installed:

### System Packages
```bash
sudo apt-get install -y \
    g++ \
    cmake \
    libboost-all-dev \
    libevent-dev \
    libdouble-conversion-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libiberty-dev \
    liblz4-dev \
    liblzma-dev \
    libsnappy-dev \
    make \
    zlib1g-dev \
    binutils-dev \
    libjemalloc-dev \
    libssl-dev \
    pkg-config \
    libunwind-dev
```

## Installation Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/facebook/folly.git
   cd folly
   ```

2. Create and enter build directory:
   ```bash
   mkdir build && cd build
   ```

3. Configure with CMake:
   ```bash
   cmake ..
   ```

4. Build the library:
   ```bash
   make -j$(nproc)
   ```

5. Run tests:
   ```bash
   make test
   ```

6. Install the library:
   ```bash
   sudo make install
   ```

## Common Issues and Troubleshooting

1. If you encounter package installation issues:
   - Ensure your system time is correctly synchronized
   - Make sure your package repositories are up to date
   - Check your internet connection

2. Build issues:
   - Verify all dependencies are correctly installed
   - Ensure you have enough disk space
   - Make sure you have sufficient RAM (at least 4GB recommended)

3. Test failures:
   - Some tests might fail due to timing-sensitive operations
   - Check system resources during test execution
   - Verify that all required dependencies are properly installed

## Notes

- Folly is a large library with many dependencies. The build process can take significant time and resources.
- Some components might require additional dependencies depending on your use case.
- Regular system maintenance and updates are recommended before attempting the installation.

## Version Information

This guide was created for the Facebook Folly library as of May 31, 2025. Please check the official repository for any updates or changes to the build process.