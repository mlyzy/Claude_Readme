# CPython Manual Deployment Guide

This guide describes the process for building and testing CPython from source.

## Prerequisites

The following packages are required to build CPython:

```bash
sudo apt-get update
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
    libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev \
    python3-openssl
```

## Build Process

1. Clone the repository:
   ```bash
   git clone https://github.com/python/cpython.git
   cd cpython
   ```

2. Configure the build:
   ```bash
   ./configure --enable-optimizations
   ```
   * The `--enable-optimizations` flag enables Profile Guided Optimization, which makes Python faster but increases build time.

3. Build CPython:
   ```bash
   make -j$(nproc)
   ```
   * This command uses all available CPU cores for parallel building
   * Build time can take 20-60 minutes depending on your system

4. Install (optional):
   ```bash
   sudo make install
   ```

## Testing

After building, you can run the test suite:

1. Run the full test suite:
   ```bash
   make test
   ```

2. Run specific tests:
   ```bash
   ./python -m test -v test_name
   ```

## Common Issues and Solutions

1. SSL Module Issues:
   * If SSL module fails to build, ensure you have `libssl-dev` installed

2. Missing Dependencies:
   * If configure fails, check that all prerequisites are installed
   * Use `apt-get build-dep python3` on Debian/Ubuntu to install all build dependencies

3. Build Performance:
   * Remove `--enable-optimizations` for faster build time (but slower Python execution)
   * Adjust `-j` parameter in make command to match your CPU capabilities

## Verification

To verify your build:

1. Check Python version:
   ```bash
   ./python --version
   ```

2. Test basic functionality:
   ```bash
   ./python -c "print('Hello, World!')"
   ```

3. Check for successful module compilation:
   ```bash
   ./python -c "import ssl; print(ssl.OPENSSL_VERSION)"
   ```

## Notes

* The build process can be resource-intensive and time-consuming
* Some tests may fail on certain platforms - consult the CPython Developer's Guide for details
* For development work, consider using the `--with-pydebug` configure option
* Keep system resources in mind when running the test suite as it can be memory-intensive