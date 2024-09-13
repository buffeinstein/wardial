# Wardial

![](https://github.com/buffeinstein/wardial/workflows/task1/badge.svg)
![](https://github.com/buffeinstein/wardial/workflows/task2/badge.svg)


**Learning Objectives:**

1. Learn to use and write async functions
1. Increase understanding of internet architecture

## Background

The [CS40 wardialing lab](https://github.com/mikeizbicki/cmc-csci040/tree/2021fall/lab-wardialing) creates a simple script to scan all computers on the North Korean internet for web servers.

We will use python's async functions to build a script that can scan arbitrary sections of the internet much faster.
For example, the following command scans all North Korean ip addresses in only 30 seconds:

```
$ time python3 wardial.py 175.45.176.0/22
INFO:root:server at http://175.45.178.161
INFO:root:server at http://175.45.176.71
INFO:root:server at http://175.45.176.91
INFO:root:server at http://175.45.176.77
INFO:root:server at http://175.45.176.83
INFO:root:server at http://175.45.176.85
total ips found = 6

real    0m32.930s
user    0m1.006s
sys 0m0.067s
```

Scanning all ip addresses that belong to the Claremont Colleges takes about 20 minutes:
```
$ time python3 wardial.py 134.173.32.22/16 --timeout=1
INFO:root:server at http://134.173.238.250
INFO:root:server at http://134.173.53.33
INFO:root:server at http://134.173.53.35
...
INFO:root:server at http://134.173.114.161
INFO:root:server at http://134.173.69.195
INFO:root:server at http://134.173.254.189
total ips found = 71

real    18m7.277s
user    16m12.539s
sys     0m3.050s
```

The `--timeout` parameter adjusts how long the program should wait for a response from a server.
There is also a parameter `--max_connections` which controls the number of servers to attempt to connect to simultaneously.
(On most machines, non-root users cannot have more than about 1000 simultaneous web connections.)
Tuning either of these parameters can improve the scanning performance.

[State of the art scanning tools are able to scan all 4 billion internet addresses in under an hour.](https://www.vice.com/en/article/kbbmyx/now-you-can-scan-the-internet-in-under-an-hour)
Getting that level of performance requires carefully tuning many other network configuration parameters as well.

**Task 1:**

The `wardial` function currently contains failing doctests,
as seen by the command:
```
$ python3 -m doctest wardial.py
```
Find the `FIXME (Task 1)` comment inside the `wardial` function,
and follow the instructions to make the doctests pass.
Note that the doctests can take up to an hour to run,
and it is okay to move onto task 2 without waiting for the doctests to finish.

**Task 2:**

Unfortunately, the code is extremely slow.
Even though we have functions labeled `async` and we are `await`ing them,
we are not doing it correctly,
and the web requests are not happening concurrently.

Find the `FIXME (Task 2)` comment inside the `_wardial_async` function,
and follow the instructions to enable concurrency.

## Submission

Once the test cases pass and the badges turn green, submit your github url to sakai.
