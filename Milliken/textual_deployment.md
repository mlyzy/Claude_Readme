# Textual Project Deployment Process

## Environment Setup
1. Clone the repository:
```bash
git clone https://github.com/Textualize/textual.git
```

2. Install system dependencies:
```bash
sudo apt-get update
sudo apt-get install -y python3-pip python3-venv
```

3. Create and activate virtual environment:
```bash
cd textual
python3 -m venv venv
source venv/bin/activate
```

## Installation
1. Install the package in editable mode:
```bash
pip install -e .
```

The basic installation was successful, with all required dependencies being installed correctly.

## Testing
The testing process revealed some additional requirements:

1. Install testing dependencies:
```bash
pip install pytest pytest-asyncio pytest-xdist
```

2. Run tests:
```bash
python -m pytest tests/
```

## Current Status
- Basic installation: ✅ Successful
- Dependencies installation: ✅ Successful
- Testing: ⚠️ Incomplete

## Issues Encountered
1. The initial attempt to install with dev dependencies (`pip install -e ".[dev]"`) failed as the dev extra was not available.
2. The testing process required additional dependencies (pytest-asyncio and pytest-xdist).
3. Tests execution was interrupted due to configuration issues with pytest markers and asyncio settings.

## Manual Deployment Steps
For a successful manual deployment, follow these steps:

1. Ensure you have Python 3.x installed
2. Clone the repository
3. Create a virtual environment
4. Install the base package: `pip install -e .`
5. For development/testing:
   - Install pytest and its plugins: `pip install pytest pytest-asyncio pytest-xdist`
   - Configure pytest with appropriate asyncio settings
   - Set up proper pytest markers configuration

## Dependencies
The project requires the following main dependencies:
- markdown-it-py[linkify,plugins]>=2.1.0
- platformdirs<5,>=3.6.0
- rich>=13.3.3
- typing-extensions<5.0.0,>=4.4.0

Additional testing dependencies:
- pytest
- pytest-asyncio
- pytest-xdist