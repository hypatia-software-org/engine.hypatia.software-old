# Installation notes for FreeBSD

How to install Hypatia on FreeBSD, including Pygame, other notes.

Tested on FreeBSD 10.1-RELEASE.

## Python 2.7

The easy way is to run the installer included with Hypatia:

```shell
$ ./install-freebsd-python2.sh
```

Otherwise you can do this:


```shell
$ sudo pkg install python27 py27-pip py27-game
$ pip install --user -r requirements/python2.txt .
```

## Python 3.4

I have not tested this!
