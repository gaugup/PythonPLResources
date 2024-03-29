[![Link check](https://github.com/gaugup/PythonPLResources/actions/workflows/linkcheck.yml/badge.svg)](https://github.com/gaugup/PythonPLResources/actions/workflows/linkcheck.yml)

# Python Programming Language Resources
Repository for resources on python programming and related frameworks

## Github actions
- [Setting up python CI via pip using Github actions](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-python)<!-- markdown-link-check-disable-line -->
- [Setting up python CI via conda using Github actions](https://autobencoder.com/2020-08-24-conda-actions/)

## Programming resources
- [Python List declaration](https://careerkarma.com/blog/how-to-initialize-a-list-in-python/)
- [Python decorators](https://www.freecodecamp.org/news/python-decorators-explained-with-examples/#:~:text=When%20to%20Use%20a%20Decorator%20in%20Python%20You%27ll,to%20run%20the%20same%20code%20on%20multiple%20functions)
- [Different ways of getting python versions](https://github.com/gaugup/PythonPLResources/blob/main/WaysToGetPythonVersion/WaysToGetPythonVersion.md)
- [Advanced Python programming concepts](https://betterprogramming.pub/must-know-python-concepts-for-experienced-developers-4554ceea3d95?gi=1b8acc80e46)
- [Python lambda expressions to sort complex lists](https://www.adamsmith.haus/python/answers/how-to-sort-a-list-with-a-lambda-expression-in-python)
- [Python `ord()` and `chr()` functions](https://datagy.io/python-ord-chr/)

## Testing
- [Pytest: testing for exceptions](https://miguendes.me/how-to-check-if-an-exception-is-raised-or-not-with-pytest)
- [Optimizing pytest runtime](https://github.com/gaugup/PythonPLResources/blob/main/OptimizingPytestRuntime/OptimizingPytestRuntime.md)

## Linting
- [Useful flake8 extensions](https://github.com/DmytroLitvinov/awesome-flake8-extensions)
- [How to create flake8 plugin](https://flake8.pycqa.org/en/latest/plugin-development/index.html)

## Microservices
- Flask Server in Python
  - [link](https://scoutapm.com/blog/python-flask-tutorial-getting-started-with-flask)
  - [link](https://www.digitalocean.com/community/tutorials/processing-incoming-request-data-in-flask)

## Performance analysis and Tuning

- Memory Profiling
  - [Python Memory Profiler](https://pypi.org/project/memory-profiler/#:~:text=%20Project%20description%20%201%20Memory%20Profiler.%20This,proc%20represents%20what...%205%20Development.%20%20More%20) Provides a python library to profile line-by-line the memory utilization of a python process.

- Memory Management
  - [Pandas Memory Management](https://charumakhijani.medium.com/pandas-memory-management-b24807d2bb15) Provides some neat suggestions on how to use optimize on memory when using pandas DataFrrame. 

- CPU profiling
  - [Profiling in Python (Detect CPU & memory bottlenecks)](https://likegeeks.com/python-profiling/) Provides a host of libraries to profile python code to identify bottlenecks.

## Creating a wheel file
- The `.whl` file of a python package having a `setup.py` can be generated va the command `python setup.py sdist bdist_wheel`. This creates a folder named `dist` which has two files with extensions `.whl` and `.tar.gz`.
