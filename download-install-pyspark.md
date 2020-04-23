# Apache Spark | setup Pyspark

## Scenario: Configure python3 to start pyspark

## Pre-reqs
Ubuntu 18.04 ships with Python 3, as the default Python installation, check if python3 is already installed using command ```python3 --version```. Use command ```sudo apt-get install python3.6``` to install latest version of Python if not already installed.  





### Steps to install pip (pip3) for Python 3:
Run ```sudo apt install python3-pip``` to install pip for Python3, check pip version using ```pip3 --version```
output should be similar to ```pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)```

## findspark
```python3 -m pip install findspark```
Output
```
Collecting findspark
  Using cached https://files.pythonhosted.org/packages/b1/c8/e6e1f6a303ae5122dc28d131b5a67c5eb87cbf8f7ac5b9f87764ea1b1e1e/findspark-1.3.0-py2.py3-none-any.whl
Installing collected packages: findspark
Successfully installed findspark-1.3.0```



## Package Managers

**pip** is a package manager that facilitates installation, upgrade, and uninstallation of python packages. It also works with virtual python environments. **conda** is also packaging tool that handles installation task (installation, upgrade and uninstallation) for both python and non-Python . And, also works with virtual system environments.

[Understanding Conda and Pip](https://www.anaconda.com/understanding-conda-and-pip/)
