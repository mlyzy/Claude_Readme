# RxJava Manual Deployment Guide

## Prerequisites

Before you can build and test RxJava, you need to have the following tools installed:

1. **Java Development Kit (JDK) 8 or later**
   - Download from: https://adoptium.net/ or https://www.oracle.com/java/technologies/downloads/
   - Set JAVA_HOME environment variable
   - Add Java to your PATH

2. **Git**
   - Download from: https://git-scm.com/downloads
   - Required for cloning the repository

## Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/ReactiveX/RxJava.git
   cd RxJava
   ```

2. **Build the Project**
   - RxJava uses Gradle as its build system
   - The project includes a Gradle wrapper, so you don't need to install Gradle separately
   - To build the project:
   ```bash
   ./gradlew build
   ```

3. **Run Tests**
   - To run all tests:
   ```bash
   ./gradlew test
   ```
   - To run specific tests:
   ```bash
   ./gradlew :rxjava:test --tests "io.reactivex.rxjava3.some.specific.TestClass"
   ```

## Project Structure

The main source code is located in the `src/main/java` directory, with the following key components:

- Core Observable types
- Operators
- Schedulers
- Subjects
- Flowable implementations

## Common Issues and Solutions

1. **Java Version Mismatch**
   - Ensure you're using a compatible Java version (8 or later)
   - Check your Java version with `java -version`
   - Update JAVA_HOME if necessary

2. **Build Failures**
   - Clean the build directory: `./gradlew clean`
   - Try rebuilding: `./gradlew build`

3. **Test Failures**
   - Run with debug logging: `./gradlew test --debug`
   - Check for environment-specific issues

## Additional Resources

- Official Documentation: https://github.com/ReactiveX/RxJava/wiki
- API Documentation: http://reactivex.io/RxJava/javadoc/
- Issue Tracker: https://github.com/ReactiveX/RxJava/issues

## Note

This document was created because the automated deployment attempt was unsuccessful due to environment setup issues. The steps above detail the manual process required to successfully build and test RxJava.