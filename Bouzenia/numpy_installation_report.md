# NumPy Installation and Testing Report

## Overview
This document summarizes the process of installing and testing NumPy, a fundamental package for scientific computing with Python.

## Installation Process

### Environment Setup
```bash
# Create a virtual environment
python3 -m venv numpy_env
source numpy_env/bin/activate

# Install required tools
pip install --upgrade pip setuptools wheel cython pytest build

# Install system dependencies
sudo apt-get install -y gcc gfortran python3-dev libblas-dev liblapack-dev
```

### Installation Methods

#### Method 1: Installing from PyPI (Successful)
```bash
pip install numpy
```

#### Method 2: Building from Source (Unsuccessful)
We attempted to build NumPy from source by cloning the repository and building it:

```bash
git clone https://github.com/numpy/numpy.git
cd numpy
python -m build
```

This method encountered issues with the build system, specifically with the meson build system:
```
meson-python: error: Could not find the specified meson: "vendored-meson/meson/meson.py"
```

Similarly, trying to install with pip in development mode failed:
```bash
pip install -e .
```

## Testing the Installation

We verified the successful installation using several tests:

### Basic Import and Version Check
```python
import numpy as np
print(np.__version__)
# Output: 2.2.6
```

### Functionality Tests
We verified that key NumPy functionality works as expected:

1. **Array Creation**
   ```python
   a = np.array([[1, 2, 3], [4, 5, 6]])
   assert a.shape == (2, 3)
   ```

2. **Linear Algebra**
   ```python
   b = np.linalg.inv(np.array([[1, 2], [3, 4]]))
   assert np.allclose(np.dot(b, np.array([[1, 2], [3, 4]])), np.eye(2))
   ```

3. **FFT (Fast Fourier Transform)**
   ```python
   c = np.fft.fft(np.array([1, 2, 3, 4]))
   assert len(c) == 4
   ```

4. **Random Number Generation**
   ```python
   d = np.random.normal(size=1000)
   assert 0.2 < np.std(d) < 5
   ```

## Conclusion

NumPy was successfully installed using pip and the functionality was verified through various tests. Building from source encountered issues with the meson build system, which would require additional configuration to resolve.

## Manual Deployment Process

If you need to manually deploy NumPy from source, here's the recommended process:

1. **Install system dependencies**
   ```bash
   sudo apt-get update
   sudo apt-get install -y git python3-dev python3-pip build-essential gcc gfortran libblas-dev liblapack-dev
   ```

2. **Set up a virtual environment**
   ```bash
   python3 -m venv numpy_env
   source numpy_env/bin/activate
   ```

3. **Install Python dependencies**
   ```bash
   pip install --upgrade pip setuptools wheel cython pytest build meson meson-python ninja
   ```

4. **Clone the NumPy repository**
   ```bash
   git clone https://github.com/numpy/numpy.git
   cd numpy
   ```

5. **Install NumPy in development mode**
   ```bash
   pip install --no-build-isolation -e .
   ```

6. **If the above fails, try these alternative methods:**
   ```bash
   # Method A: Using setup.py directly
   python setup.py build
   python setup.py install

   # Method B: Using pip with build isolation disabled
   pip install --no-build-isolation .
   ```

7. **Verify the installation**
   ```bash
   python -c "import numpy as np; print(np.__version__)"
   python -c "import numpy as np; a = np.array([1, 2, 3]); print(a)"
   ```