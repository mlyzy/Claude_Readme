# MPV Player Installation and Testing Process

## Overview
This document describes the process of downloading, building, and testing the mpv media player from the official GitHub repository: https://github.com/mpv-player/mpv

## System Requirements
- Ubuntu Linux
- Build tools (gcc, meson, ninja)
- FFmpeg libraries (version >= 60.31.102)
- Various development libraries for audio, video, and GUI

## Installation Process

### 1. Cloning the Repository
```bash
git clone https://github.com/mpv-player/mpv.git
```

### 2. Installing Dependencies
The following dependencies are required to build mpv:

- Basic build tools:
```bash
sudo apt-get install -y build-essential meson ninja-build pkg-config python3-pip
```

- FFmpeg libraries (requires newer versions than in Ubuntu repositories):
```bash
git clone --depth 1 https://git.ffmpeg.org/ffmpeg.git
cd ffmpeg
./configure --prefix=/usr/local --enable-shared
make -j$(nproc)
sudo make install
```

- Other essential libraries:
```bash
sudo apt-get install -y libx11-dev libxrandr-dev libxss-dev libxext-dev \
  libvdpau-dev libgl1-mesa-dev zlib1g-dev libass-dev liblua5.2-dev
```

- libplacebo (using Git subproject):
```bash
mkdir -p subprojects
git clone https://code.videolan.org/videolan/libplacebo.git --depth=1 --recursive subprojects/libplacebo
```

### 3. Building MPV
```bash
cd mpv
meson setup build
meson compile -C build
```

### 4. Installing MPV
```bash
sudo meson install -C build
```

## Testing Process
After installation, test basic functionality:

```bash
mpv --version
mpv /path/to/video/file.mp4
```

## Challenges Encountered
- Meson version in Ubuntu repositories is too old (requires >=1.3.0)
- FFmpeg libraries in Ubuntu repositories are too old (requires >= 60.31.102)
- Several package dependencies have connectivity issues
- Vulkan header compatibility issues with the newer FFmpeg version causing build failures
- Incompatibilities between libplacebo and FFmpeg causing build errors with hwcontext_vulkan.h
- Missing Vulkan development headers for proper library integration

## Manual Deployment Instructions
If the automated installation process fails, follow these steps:

1. Clone the repositories:
```bash
git clone https://github.com/mpv-player/mpv.git
git clone --depth 1 https://git.ffmpeg.org/ffmpeg.git
```

2. Build and install FFmpeg from source:
```bash
cd ffmpeg
./configure --prefix=/usr/local --enable-shared
make -j$(nproc)
sudo make install
sudo ldconfig
```

3. Set up libplacebo as a subproject:
```bash
cd ../mpv
mkdir -p subprojects
git clone https://code.videolan.org/videolan/libplacebo.git --depth=1 --recursive subprojects/libplacebo
```

4. Install Meson from pip:
```bash
pip3 install --user meson --upgrade
export PATH="$HOME/.local/bin:$PATH"
```

5. Build and install mpv with specific configurations to avoid Vulkan-related issues:
```bash
# Try with disabled features to bypass compatibility issues
meson setup build \
  -Dvulkan=disabled \
  -Degl=disabled \
  -Dlibmpv=false \
  -Dcplayer=true \
  -Dopengl=disabled

# If the above fails, you can try to build with minimal features
meson setup build -Dvulkan=disabled -Degl=disabled -Dopengl=disabled -Dx11=disabled -Dgl=disabled

# Compile with the configured settings
meson compile -C build
sudo meson install -C build
```

6. Test the installation:
```bash
mpv --version
```

## Alternative Installation Methods

If building from source is too problematic, consider these alternatives:

1. **Use the package manager** - On Ubuntu/Debian:
   ```bash
   sudo apt install mpv
   ```
   Note: This will install an older version that is compatible with your system's libraries.

2. **Use Flatpak** - For the latest stable version:
   ```bash
   sudo apt install flatpak
   flatpak install flathub io.mpv.Mpv
   ```

3. **Use AppImage** - Download and use a portable version:
   ```bash
   # Find the latest AppImage on the mpv releases page
   # Make it executable and run it
   chmod +x mpv-*.AppImage
   ./mpv-*.AppImage
   ```

4. **Use snap** - Install via snap package:
   ```bash
   sudo snap install mpv
   ```

Each method has advantages and disadvantages regarding feature availability, integration with the system, and ease of updates.