# Installation notes for Linuxmint

Installation notes for installing Hypatia on Linuxmint.

## Python 2.7

### The Easy Way

Simply run the installer included with Hypatia:

```shell
$ ./install-linuxmint-py27.sh
```

### The hard way

Install pygame, pyganim, PIL

```shell
$ sudo apt-get install python-pygame
```

```shell
$ pip install --user -r requirements/python2.txt .
```

## Python 3.4

### The Easy Way

Simply run the installer included with Hypatia:

```shell
$ ./install-linuxmint-python3.sh
```

### The hard way

Save the following script as `install.sh`, then `chmod +x install.sh` and `sudo ./install`.

This shell script installs all of the dependencies required:

```shell
# install depends
sudo apt-get install python3-pip python3-dev libsdl1.2-dev\
     libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev\
     libsdl-gfx1.2-dev libsdl-net1.2-dev libsdl-image1.2-dev\
     libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsmpeg-dev\
     libsdl1.2-dev libportmidi-dev libswscale-dev libavformat-dev\
     libavcodec-dev libsdl-sge-dev libsdl-sound1.2-dev\
     libportmidi-dev libsmpeg-dev
pip3 install --user Image pyganim

# compile pygame
hg clone https://bitbucket.org/pygame/pygame
cd pygame
python3 setup.py build
cd ..
pip3 install --user -r requirements/python3.txt .
```
