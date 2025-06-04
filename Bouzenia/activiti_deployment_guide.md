# Activiti Deployment Guide

This document outlines the process for deploying and testing the Activiti project, based on our attempts to build and run the code from GitHub.

## Overview

[Activiti](https://github.com/Activiti/Activiti) is a light-weight workflow and Business Process Management (BPM) Platform for Java. It provides a robust BPMN 2 process engine that can be integrated into any Java application.

## Prerequisites

Based on our analysis of the project, the following prerequisites are required:

1. **Java Development Kit (JDK) 21**
   - The project explicitly requires Java 21 (as specified in the POM file)
   - Can be installed with: `sudo apt-get install openjdk-21-jdk`

2. **Maven 3.x**
   - Required for building the project
   - Can be installed with: `sudo apt-get install maven`

3. **Git**
   - For cloning the repository
   - Can be installed with: `sudo apt-get install git`

## Step 1: Clone the Repository

```bash
git clone https://github.com/Activiti/Activiti.git
cd Activiti
```

## Step 2: Build the Core Modules

The project follows a modular structure. Before building examples or applications, you need to build the core modules:

```bash
# Install the parent POM and core modules
mvn clean install -DskipTests -T 1C

# If the above command fails, try building modules individually
cd activiti-api
mvn clean install -DskipTests

cd ../activiti-core-common
mvn clean install -DskipTests

cd ../activiti-core
mvn clean install -DskipTests

cd ../activiti-dependencies
mvn clean install -DskipTests
```

Note: The `-DskipTests` flag is used to skip tests during the initial build. Once the build is successful, you can run the tests separately.

## Step 3: Build and Run Examples

Activiti provides several examples that demonstrate its capabilities. After building the core modules, you can build and run the examples:

```bash
cd activiti-examples/activiti-api-basic-process-example
mvn clean package
mvn spring-boot:run
```

This will start a Spring Boot application that demonstrates a simple process workflow.

## Step 4: Running Tests

To run the tests for the project:

```bash
# Run all tests
mvn test

# Run tests for a specific module
cd activiti-core
mvn test
```

## Common Issues and Troubleshooting

1. **Dependency Resolution Issues**
   - If you encounter dependency resolution issues, check your Maven settings.xml file
   - The project includes a settings.xml file that can be used: `-s settings.xml`

2. **Network Timeouts**
   - If you experience network timeouts while downloading dependencies, try increasing the timeout settings:
   ```
   mvn -Dmaven.wagon.http.timeout=60000 -Dmaven.wagon.http.pool=false clean install
   ```

3. **Java Version Mismatch**
   - Ensure you're using Java 21 as required by the project
   - Verify with: `java -version`

4. **Memory Issues**
   - If you encounter memory issues during the build, increase the memory allocated to Maven:
   ```
   export MAVEN_OPTS="-Xmx2g -XX:MaxPermSize=512m"
   ```

## Project Structure

The Activiti project consists of several modules:

1. **activiti-api**: Core API definitions
2. **activiti-core-common**: Common functionality used across the project
3. **activiti-core**: Core process engine implementation
4. **activiti-examples**: Example applications demonstrating usage
5. **activiti-dependencies**: Dependency management

## Running in Production

For production deployment, consider the following:

1. **Database Configuration**: By default, examples use H2 in-memory database. For production, configure a persistent database (MySQL, PostgreSQL, etc.)

2. **Security Configuration**: Implement proper security measures beyond the basic authentication included in examples

3. **Monitoring and Management**: Implement monitoring and management tools for observing workflow processes

4. **Clustering**: For high availability, consider deploying multiple instances with proper load balancing

## Additional Resources

- [Activiti Website](https://www.activiti.org/)
- [Official Documentation](https://www.activiti.org/documentation)
- [GitHub Repository](https://github.com/Activiti/Activiti)