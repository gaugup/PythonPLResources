# Optimizing pytest runtime

In all these years as a software developer I have experienced that the throughput of some task in any piece of software is paramount for customers. If the software that you ship cannot scale and meet the necessary customer requirements, then there are chances that you might eventually loose that customer. Time and again as software developers, we work on scaling the software better to satisfy such customer demands. But as software developers do invest enough time and thought to run our tests faster?

Writing tests is a mandatory requirement for all software developers. As developers we are expected write unit and integration tests that are robust, less brittle (less likely to break) and provide good code coverage. But do we think that our tests should run faster? Why should tests run faster anyways? If you haven't thought about these questions then probably slower tests haven't frustrated you as much as they annoy me. 

I treat slow tests as a form of technical debt which eventually catches up with a development team. Slow tests mean longer run times for a dev-ops pipeline which means it takes longer for a developer pull request to merge into the code base. If developer pull requests take longer to run, then it invariably slows down the feature velocity and adds on to unnecessary delays for developer's features to finish and potentially leads to missing of deadlines.

Being a python developer, I run most tests using pytest testing framework. The pytest testing framework provides many extensions using which we can run the tests in parallel, enforce failing of tests if the tests exceed a particular time limit and also helps in logging of run time of the tests. I found these capabilities in pytest particularly useful in debugging which tests longer to run and save time while running a whole suit of tests. 

So get started on learning about the aforementioned  pytest extensions, let's look at a sample test file which contains a few slow tests. Below is the sample test file:-
```python
import time


class Test:

    def test_fastest(self):
        time.sleep(5)
        assert True

    def test_slow(self):
        time.sleep(40)
        assert True

    def test_slowest(self):
        time.sleep(100)
        assert True

```

When we run the tests in this file using pytest, we see a runtime of roughly 140 seconds. 140 seconds is a lot for running three tests using pytest!

```c
pytest test_pytest.py
==================================================== test session starts ====================================================
platform win32 -- Python 3.6.12, pytest-6.2.4, py-1.10.0, pluggy-0.13.1
rootdir: C:\Users\gaugup\Documents\WRITE UPS\Pytest
collected 3 items

test_pytest.py ...                                                                                                     [100%]

=============================================== 3 passed in 145.07s (0:02:25) ===============================================

```

## Finding the most time consuming tests
`pytest` allows the ` - durations` parameter to find the most time consuming test(s). Running the tests in the `pytest` test file again with ` - durations` set as 10 we can see that the test `test_slowest` takes the maximum time.
```c
pytest - durations=10 test_pytest.py
================================================= test session starts =================================================
platform win32 - Python 3.7.11, pytest-5.0.1, py-1.11.0, pluggy-0.13.1
rootdir: C:\Users\gaugup\Documents\WRITE UPS\Pytest
plugins: nbval-0.9.6, cov-3.0.0, mock-3.1.1
collected 3 items
test_pytest.py … [100%]
============================================== slowest 10 test durations ==============================================
100.01s call test_pytest.py::Test::test_slowest
40.01s call test_pytest.py::Test::test_slow
5.01s call test_pytest.py::Test::test_fastest
(0.00 durations hidden. Use -vv to show these durations.)
============================================= 3 passed in 145.10 seconds ==============================================
```
## Running tests in parallel
Now that we have established how much time is spent in each test, let's look into some extensions that `pytest` has provided to optimize the tests. `pytest` provides the extension [pytest-xdist](https://pypi.org/project/pytest-xdist/) which allows us to run python tests in parallel. You can install `pytest-xdist` using pip in your python environment.
```c
pip install pytest-xdist
```
We can now run the above tests in parallel using the following command line option `-n`.
```c
pytest - durations=10 -n 3 test_pytest.py
============================================== test session starts ==============================================
platform win32 - Python 3.7.11, pytest-7.1.1, pluggy-0.13.1
rootdir: C:\Users\gaugup\Documents\WRITE UPS\Pytest
plugins: nbval-0.9.6, cov-3.0.0, forked-1.4.0, mock-3.1.1, xdist-2.5.0
gw0 [3] / gw1 [3] / gw2 [3]
… [100%]
============================================= slowest 10 durations ==============================================
100.00s call test_pytest.py::Test::test_slowest
40.00s call test_pytest.py::Test::test_slow
5.00s call test_pytest.py::Test::test_fastest
(6 durations < 0.005s hidden. Use -vv to show these durations.)
========================================= 3 passed in 102.46s (0:01:42) =========================================
```
From the above execution of the three tests took about 100 seconds. The pytest framework was able to spin up three workers and run each of the three tests in parallel on each worker, thus optimizing the total run time. The individual tests still took the same amount of time to run but since the tests ran in parallel the overall time was less.
## Adding timeout on tests
It is also possible to fail a particular test that is executed using `pytest` if that particular test takes longer than usual. The `pytest` plugin [pytest-timeout](https://pypi.org/project/pytest-timeout/) allows to fail a particular test if that test exceeds the timeout value. You can install `pytest-timeout` using pip in your python environment.
```
pip install pytest-timeout
```
We can now run the above tests in with a specified value of timeout (50 seconds in the example below) using the `pytest` command line option ` - timeout`.
```
pytest - timeout=50 test_pytest.py
============================================== test session starts ==============================================
platform win32 - Python 3.7.11, pytest-7.1.1, pluggy-0.13.1
rootdir: C:\Users\gaugup\Documents\WRITE UPS\Pytest
plugins: nbval-0.9.6, cov-3.0.0, forked-1.4.0, mock-3.1.1, timeout-2.1.0, xdist-2.5.0
timeout: 50.0s
timeout method: thread
timeout func_only: False
collected 3 items
test_pytest.py ..
++++++++++++++++++++++++++++++++++++++++++++++++++++ Timeout +++++++++++++++++++++++++++++++++++++++++++++++++++++
```
As it can be seen in the above output that two of the three tests (`test_fastest` takes 5 seconds to run and `test_clow` takes 40 seconds to run) passed while one test failed (`test_slowest` takes 100 seconds to run) due to timeout.
To summarize, in the above article we went through the following:-
- How to find which are the most time consuming tests when running tests using `pytest`.
- How to run tests in parallel using the `pytest` plugin `pytest-xdist`.
- How to put timeout on `pytest` tests using the `pytest-timeout` plugin.
