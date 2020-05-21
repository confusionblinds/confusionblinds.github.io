# Apache Spark | setup Pyspark

## Scenario: Configure python3 to start pyspark

## Pre-reqs
Ubuntu 18.04 ships with Python 3, as the default Python installation, check if python3 is already installed using command ```python3 --version```. Use command ```sudo apt-get install python3.6``` to install latest version of Python if not already installed.  





### Steps to install pip (pip3) for Python 3:
Run ```sudo apt install python3-pip``` to install pip for Python3, check pip version using ```pip3 --version```
output should be similar to ```pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)```

## findspark
```python3 -m pip install findspark
```

Output
```
Collecting findspark
  Using cached https://files.pythonhosted.org/packages/b1/c8/e6e1f6a303ae5122dc28d131b5a67c5eb87cbf8f7ac5b9f87764ea1b1e1e/findspark-1.3.0-py2.py3-none-any.whl
Installing collected packages: findspark
Successfully installed findspark-1.3.0
```

## Package Managers

**pip** is a package manager that facilitates installation, upgrade, and uninstallation of python packages. It also works with virtual python environments. **conda** is also packaging tool that handles installation task (installation, upgrade and uninstallation) for both python and non-Python . And, also works with virtual system environments.

[Understanding Conda and Pip](https://www.anaconda.com/understanding-conda-and-pip/)


## Installing Anaconda


## Where is Python conda all installed?

```
(base) sunil@kcubuntu:~$ whereis conda
conda: /opt/anaconda3/bin/conda /opt/anaconda3/condabin/conda

(base) sunil@kcubuntu:~$ whereis python
python: /usr/bin/python2.7 /usr/bin/python3.6 /usr/bin/python3.6-config /usr/bin/python3.6m-config /usr/bin/python /usr/bin/python3.6m /usr/lib/python2.7 /usr/lib/python3.7 /usr/lib/python3.6 /usr/lib/python3.8 /etc/python2.7 /etc/python3.6 /etc/python /usr/local/lib/python2.7 /usr/local/lib/python3.6 /usr/include/python3.6 /usr/include/python3.6m /usr/share/python /opt/anaconda3/bin/python3.7 /opt/anaconda3/bin/python3.7m-config /opt/anaconda3/bin/python3.7-config /opt/anaconda3/bin/python /opt/anaconda3/bin/python3.7m /usr/share/man/man1/python.1.gz

(base) sunil@kcubuntu:~$ whereis python3
python3: /usr/bin/python3.6 /usr/bin/python3.6-config /usr/bin/python3.6m-config /usr/bin/python3.6m /usr/bin/python3 /usr/lib/python3.7 /usr/lib/python3.6 /usr/lib/python3.8 /usr/lib/python3 /etc/python3.6 /etc/python3 /usr/local/lib/python3.6 /usr/include/python3.6 /usr/include/python3.6m /usr/share/python3 /opt/anaconda3/bin/python3.7 /opt/anaconda3/bin/python3.7m-config /opt/anaconda3/bin/python3.7-config /opt/anaconda3/bin/python3.7m /opt/anaconda3/bin/python3 /usr/share/man/man1/python3.1.gz


(base) sunil@kcubuntu:~$ whereis anaconda
anaconda: /opt/anaconda3/bin/anaconda
```

## Python Virtual Envrionment : Isolated python virtual environment that can be customized per project.

### Why ?
By Default all python packages are installed to a single directory on the system, which can become a problem when building multiple python projects that has different and potential conflicting depends, this problem can be solve y busing  Virtual Environment.

### How ?
Create new Directory for each Virtual Environment. links copies of Python executable, Library and Tools




