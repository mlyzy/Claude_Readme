# Apache Flink Deployment Guide

This guide provides instructions for manually deploying and testing Apache Flink.

## Prerequisites

1. **Java Development Kit (JDK)**
   - Required version: JDK 11 or later
   - Installation on Ubuntu:
     ```bash
     sudo apt-get update
     sudo apt-get install openjdk-11-jdk
     ```
   - Verify installation:
     ```bash
     java -version
     ```

2. **Maven**
   - Required for building Flink
   - Installation on Ubuntu:
     ```bash
     sudo apt-get install maven
     ```
   - Verify installation:
     ```bash
     mvn -version
     ```

## Building Flink from Source

1. **Clone the Repository**
   ```bash
   git clone https://github.com/apache/flink.git
   cd flink
   ```

2. **Build Flink**
   ```bash
   mvn clean install -DskipTests
   ```
   - This command builds Flink without running tests
   - For a complete build including tests, remove `-DskipTests`
   - The build process may take several minutes

3. **Build Result**
   - After successful build, you can find the binary distribution under:
     ```
     flink-dist/target/flink-<version>-bin/flink-<version>
     ```

## Starting Flink

1. **Start the Local Cluster**
   ```bash
   ./bin/start-cluster.sh
   ```

2. **Verify the System**
   - Access the Flink Web UI at http://localhost:8081
   - The web interface provides information about running jobs, task managers, and system metrics

## Running Tests

1. **Run Unit Tests**
   ```bash
   mvn test
   ```

2. **Run Integration Tests**
   ```bash
   mvn verify
   ```

## Common Issues and Troubleshooting

1. **Memory Issues During Build**
   - If you encounter memory issues during the build, you can set Maven options:
     ```bash
     export MAVEN_OPTS="-Xmx2g -XX:MaxPermSize=512m"
     ```

2. **Port Conflicts**
   - Flink uses ports 8081 (web UI) and 6123 (JobManager)
   - Ensure these ports are available or configure different ports in conf/flink-conf.yaml

3. **Java Version Mismatch**
   - Ensure you're using a compatible Java version
   - Check both JAVA_HOME and the active Java version

## Additional Resources

1. Official Documentation: https://nightlies.apache.org/flink/flink-docs-stable/
2. GitHub Repository: https://github.com/apache/flink
3. Flink User Mailing List: user@flink.apache.org

## Note
This is a basic deployment guide. Depending on your specific use case, you might need to:
- Configure additional parameters
- Set up specific connectors
- Configure high availability
- Set up monitoring and logging
- Configure memory and resource allocation

Please refer to the official documentation for more detailed information about these aspects.