# spaCy Installation and Testing Process

## Environment Setup
1. Created a new directory for the project
2. Cloned the spaCy repository from GitHub:
   ```bash
   git clone https://github.com/explosion/spaCy.git
   ```

## Installation Steps
1. Installed system dependencies:
   ```bash
   sudo apt-get update
   sudo apt-get install -y python3-pip python3-dev build-essential
   ```

2. Created and activated a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Installed build dependencies:
   ```bash
   pip install -U pip setuptools wheel
   ```

4. Installed project requirements:
   ```bash
   pip install -r requirements.txt
   ```

5. Installed spaCy in development mode:
   ```bash
   pip install -e .
   ```

6. Downloaded the English language model:
   ```bash
   python -m spacy download en_core_web_sm
   ```

## Testing Process
1. Created a test script to verify basic functionality:
   - Tested tokenization
   - Tested named entity recognition
   - Tested part-of-speech tagging

2. Test Results:
   - All basic functionality tests passed successfully
   - Core features (tokenization, NER, POS tagging) working as expected

## Verification
The installation was successful, and basic functionality was verified through our test script. The following components were tested and confirmed working:
- Core spaCy library installation
- Language model loading
- Basic NLP pipeline functionality (tokenization, NER, POS tagging)

## Additional Notes
- The installation process was smooth with no major issues
- All dependencies were resolved successfully
- The English language model (en_core_web_sm) was installed and loaded correctly
- Basic NLP functionalities are working as expected