# 1.2 Installation

AutoOptLib is downloadable at [https://github.com/auto4opt/AutoOpt](https://github.com/auto4opt/AutoOpt). The project ships both Matlab and Python implementations; choose the workflow that matches your environment. Users can use, redistribute, and modify it under the terms of the GNU General Public License v3.0.

**Matlab.** Use Matlab R2018 or newer (R2020a or higher is recommended for invoking AutoOptLib’s GUI). Required toolboxes include Statistics and Machine Learning, Communications, DSP System, Parallel Computing, and Signal Processing. After cloning the repository, add the root directory to the Matlab path.

**Python.** The Python port lives under `src/autooptlib` and targets Python 3.9 or newer. A typical installation from the project root is:

```bash
python -m pip install --upgrade pip
python -m pip install -e .
python -m pip install numpy pytest  # key runtime/test dependencies
```

You can then run `pytest` at the project root to verify the Python installation.
