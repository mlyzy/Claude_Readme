# Torch-Pruning Deployment Guide

## System Requirements

1. Python 3.x
2. pip (Python package installer)
3. Git

## Dependencies

The following Python packages are required:
- PyTorch
- torchvision
- numpy

## Installation Steps

1. Create and activate a virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate
```

2. Install PyTorch and torchvision:
```bash
pip3 install torch torchvision
```

3. Install Torch-Pruning:
```bash
pip3 install git+https://github.com/VainF/Torch-Pruning.git
```

## Manual Installation Steps (Alternative)

If the pip installation doesn't work, you can install manually:

1. Clone the repository:
```bash
git clone https://github.com/VainF/Torch-Pruning.git
cd Torch-Pruning
```

2. Install in development mode:
```bash
pip3 install -e .
```

## Testing

To verify the installation:

1. Import the package in Python:
```python
import torch_pruning as tp
```

2. Run the example scripts from the examples directory:
```bash
cd examples
python3 group_pruning.py
```

## Known Issues

1. The package might not expose a __version__ attribute
2. Make sure you have sufficient disk space and memory for PyTorch installation
3. Ensure you have CUDA support if you plan to use GPU acceleration

## Troubleshooting

1. If you encounter import errors:
   - Verify that all dependencies are installed
   - Check if the virtual environment is activated
   - Try reinstalling the package

2. If examples fail to run:
   - Ensure you're in the correct directory
   - Verify all required dependencies are installed
   - Check Python version compatibility

## Additional Resources

- Official Repository: https://github.com/VainF/Torch-Pruning
- PyTorch Installation Guide: https://pytorch.org/get-started/locally/