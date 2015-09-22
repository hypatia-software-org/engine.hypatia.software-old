# Purpose

This document is a guide for installing Hypatia on Windows.

To see which versions of Windows are supported, [[Platform-Support]].

# Nonprogrammers

For Windows, if you don't want to do any programming: [hypatia-demo-windows-current.zip](http://lillian-lemmer.github.io/hypatia/releases/hypatia-demo-windows-current.zip). It's a standalone executable; you just extract the archive and run _game.exe_.

# Programmers

## Installing Python

[Download the latest version of Python 3.x for Windows](https://www.python.org/downloads/), e.g., [Python 3.4.3](https://www.python.org/ftp/python/3.4.3/python-3.4.3.msi), and install it. The setup defaults of the are fine; you can click _next_ until the wizard finishes.

## Installing Requirements

Open the _command prompt_ and type:

```shell
C:\Python34\Scripts\pip.exe install requirements/base.txt
C:\Python34\Scripts\pip.exe install requirements/python3.txt
```

## Installing Pygame

Download the appropriate pygame _whl_ file from [this section on Christoph Gohlke's _Python Extension Packages for Windows_](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pygame), or [download a Windows installer from the Pygame website](http://www.pygame.org/download.shtml).

If you chose the _whl_ method, good for you! If not, you can skip the rest of this section

Open a command prompt in the directory which contains the _whl_ file (shift + right click, choose _open command window here_) and execute this command *IN THE SAME DIRECTORY WHICH CONTAINS `setup.py`*:

```shell
C:\Python34\Scripts\pip.exe install -r pygame-1.9.2a0-cp34-none-amd64.whl .
```

## Install Hypatia

```shell
C:\Python34\Scripts\pip.exe install .
```
