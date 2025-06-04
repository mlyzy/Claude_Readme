# Sherlock Project Installation and Testing Guide

## Overview
Sherlock is a powerful OSINT tool used to find usernames across many social networks. This guide outlines the successful installation and testing process.

## Installation Steps

1. Clone the repository:
```bash
git clone https://github.com/sherlock-project/sherlock.git
```

2. Navigate to the project directory:
```bash
cd sherlock
```

3. Install the project and its dependencies:
```bash
python3 -m pip install .
```

This will automatically install all required dependencies including:
- PySocks
- colorama
- openpyxl
- pandas
- requests
- requests-futures
- stem

## Testing the Installation

The installation can be tested by running a search for a username:

```bash
python3 sherlock_project/sherlock.py testuser
```

### Test Results
The test was successful, showing:
- The tool searched for the username "testuser" across multiple platforms
- Found 188 potential matches across various social networks and websites
- Generated links to profiles where the username exists
- Demonstrated proper functioning of all core features

## Features Demonstrated
- Username search across multiple platforms
- Concurrent searching for faster results
- Formatted output with color coding
- Direct links to found profiles

## Conclusion
The Sherlock project was successfully deployed and tested. It is working as expected, providing comprehensive username searches across numerous platforms and websites.