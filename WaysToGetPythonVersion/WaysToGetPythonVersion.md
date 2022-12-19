# Different ways of getting python version

We all know to find the version of python in a python virtual environment using command prompt.

```c
>>> python --version

Python 3.7.6 :: Anaconda, Inc.
```

However, many a times we need to consume the python version inside a python module. Fortunately, python modules **sys** and **platform** allow us to get the python versions in a nice programmable interface. Let's take a look how.

## Getting python version using **sys** module
Using the `sys` module we can get the python version using the code below:-

```python
import sys
python_version = sys.version_info
```

The above code snippet produces the python version consumable a tuple.

```c
>>> python_version
sys.version_info(major=3, minor=7, micro=6, releaselevel='final', serial=0)
>>> python_version[0]
3
>>> python_version[1]
7
>>> python_version[2]
6
```

## Getting python version using `platform` module
Using the `platform` module we can get the python version using the code below:-

```python
import platform
python_version = platform.python_version()
```

The above code snippet produces the python version consumable a string.

```c
>>> python_version
'3.7.6'
```

There is not much to choose from the above two methods to get the python version. The method described using `sys` module gives more flexibility in terms of inspecting the **major**, **minor** and **patch** versions of python whereas the method described using the `platform` module is more restrictive as it just gives the python version as a bare string. In order to extract the major, minor and patch version from this string, one has to spend some time composing the tedious regular expressions.
