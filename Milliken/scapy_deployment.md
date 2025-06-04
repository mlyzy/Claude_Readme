# Scapy Installation and Testing Process

## Successful Installation Process

1. Clone the repository:
```bash
git clone https://github.com/secdev/scapy.git
```

2. Create and activate a Python virtual environment:
```bash
cd scapy
python3 -m venv venv
source venv/bin/activate
```

3. Install Scapy:
```bash
pip install .
```

4. Basic functionality test:
```python
from scapy.all import *
print(IP())  # Successfully prints default IP packet
```

## Requirements for Manual Deployment

1. System Requirements:
   - Python 3.x
   - python3-pip
   - python3-venv
   - tcpdump (for packet capture capabilities)

2. Optional Dependencies:
   - pytest (for running tests)
   - Additional dependencies may be required for specific features:
     - cryptography (for encryption related features)
     - matplotlib (for plotting)
     - pyx (for postscript/pdf generation)

3. Testing Framework:
   - The project includes a comprehensive test suite in the `/test` directory
   - Tests can be run using the `run_tests` script in the test directory
   - Various test categories are available:
     - Unit tests
     - Regression tests
     - Contribution tests
     - Layer-specific tests

4. Usage Notes:
   - Root/sudo privileges may be required for some network operations
   - Some features may require additional system permissions
   - Certain tests may need specific network conditions or hardware

5. Documentation:
   - Comprehensive documentation is available in the `/doc` directory
   - Examples and use cases can be found in the test files (*.uts)

The installation was successful, and basic functionality is working. However, running the full test suite requires additional setup and permissions that may vary depending on the system configuration and requirements.