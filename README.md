# PyOptiX

Python bindings for OptiX 7.

## Installation


### Dependencies

#### OptiX SDK
Install [OptiX SDK](https://developer.nvidia.com/designworks/optix/download) version 7.6 or newer.

#### CUDA SDK
Install [CUDA SDK](https://developer.nvidia.com/cuda-downloads) version 12.6 or newer required for examples, otherwise as required by your OptiX SDK.

#### Build system requirements:
* [cmake](https://cmake.org/)
* [pip](https://pypi.org/project/pip/)

#### Code sample dependencies
To run the PyOptiX examples or tests, the python modules specified in `PyOptiX/requirements.txt` must be installed:
* pytest
* cupy
* numpy
* Pillow
* cuda-python 

### Virtual Environment
In most cases, it makes sense to setup a python environment.  Below are examples of how to setup your environment via either`Conda` or `venv`.

#### `venv` Virtual Environment
Create and activate a new virtual environment:
```
python3 -m venv env
source env/bin/activate
```
Install all dependencies:
```
pip install -r requirements.txt
```

#### Conda Environment
Create an environment containing pre-requisites:
```
conda create -n pyoptix python numpy conda-forge::cupy pillow pytest
```
Activate the environment:
```
conda activate pyoptix
```
The `pynvrtc` dependency, necessary for running the examples, needs to be installed via pip:
```
pip install pynvrtc
```

``` bash
conda create --name optix-py39 python=3.9
conda activate optix-py39
pip install pytest cupy-cuda12x numpy Pillow cuda-python
```

### Building and installing the `optix` Python module
Point `setuptools/CMake` to Optix by setting the following environment variable.

Linux:
``` bash
export PYOPTIX_CMAKE_ARGS="-DOptiX_INSTALL_DIR=<optix install dir>"
# Optix 9.0.0 requires an R570+ driver
export PYOPTIX_CMAKE_ARGS="-DOptiX_INSTALL_DIR=/home/tge/software/NVIDIA-OptiX-SDK-9.0.0-linux64-x86_64" 
# Optix 8.0.0
export PYOPTIX_CMAKE_ARGS="-DOptiX_INSTALL_DIR=/home/tge/workspace/artifacts/RTSpMSpM/optixSpMSpM"
```
Windows:
```
set PYOPTIX_CMAKE_ARGS=-DOptiX_INSTALL_DIR=C:\ProgramData\NVIDIA Corporation\OptiX SDK 7.0.0
```

Build and install using `pip` and `setuptools.py`:
``` bash
cd optix
# pip install .
pip install -e .
```

When compiling against an Optix 7.0 SDK an additional environment variable needs to be set
containing a path to the system's stddef.h location. E.g.
```
export PYOPTIX_STDDEF_DIR="/usr/include/linux"
```

## Running the Examples

Run the `hello` sample:
```
cd examples
python hello.py
```
If the example runs successfully, a green square will be rendered.

## Running the Test Suite

Test tests are using `pytest` and can be run from the test directory like this:
```
cd test
python -m pytest
```
