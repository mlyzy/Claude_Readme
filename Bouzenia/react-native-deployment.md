# React Native Project Deployment Guide

## Prerequisites

To deploy a React Native project, you need the following prerequisites:

1. Node.js and npm (Node Package Manager)
2. Java Development Kit (JDK)
3. Android Studio and Android SDK (for Android development)
4. Xcode (for iOS development - Mac only)
5. Python
6. Git

## Manual Deployment Steps

### 1. System Setup

```bash
# Update package manager
sudo apt-get update

# Install Node.js and npm
sudo apt-get install nodejs npm

# Install Java Development Kit
sudo apt-get install openjdk-11-jdk

# Install build essentials
sudo apt-get install build-essential

# Install Python
sudo apt-get install python3 python3-pip

# Verify installations
node --version
npm --version
java --version
python3 --version
```

### 2. React Native CLI Installation

```bash
npm install -g react-native-cli
```

### 3. Android Development Setup

1. Download and install Android Studio
2. Install Android SDK through Android Studio
3. Configure environment variables:
   ```bash
   export ANDROID_HOME=$HOME/Android/Sdk
   export PATH=$PATH:$ANDROID_HOME/tools
   export PATH=$PATH:$ANDROID_HOME/tools/bin
   export PATH=$PATH:$ANDROID_HOME/platform-tools
   ```

### 4. Clone and Setup React Native Repository

```bash
# Clone the repository
git clone https://github.com/facebook/react-native.git

# Navigate to the project directory
cd react-native

# Install dependencies
npm install

# Install additional development dependencies
npm install --save-dev @babel/core @babel/runtime @react-native-community/eslint-config
```

### 5. Building and Testing

```bash
# Run tests
npm test

# Start Metro bundler
npx react-native start

# Run on Android (in a separate terminal)
npx react-native run-android

# Run on iOS (Mac only)
npx react-native run-ios
```

## Common Issues and Solutions

1. Metro bundler issues:
   - Clear Metro bundler cache: `npx react-native start --reset-cache`
   - Ensure all dependencies are properly installed

2. Android build issues:
   - Ensure ANDROID_HOME is properly set
   - Update Android SDK tools
   - Check gradle version compatibility

3. Dependencies issues:
   - Clear npm cache: `npm cache clean --force`
   - Delete node_modules and reinstall: `rm -rf node_modules && npm install`

## Additional Resources

- [Official React Native Documentation](https://reactnative.dev/docs/getting-started)
- [React Native GitHub Repository](https://github.com/facebook/react-native)
- [React Native Community](https://reactnative.dev/community/overview)

Note: This guide was created on June 1, 2025, based on the current React Native deployment requirements and best practices.