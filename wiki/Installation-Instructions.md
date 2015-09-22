See also: [[Platform-Support]].

# Dependencies

Hypatia has the following dependencies:

  * Pygame
  * PIL/Pillow
  * pyganim

# Windows + Nonprogrammer

Windows users can simply download [the current Windows standalone (.zip)](https://lillian-lemmer.github.io/hypatia/releases/hypatia-demo-windows-current.zip) if they don't wish to do any programming.

# Using an Install Script

The following table illustrates which OS/python combinations have an install script made for it. These install scripts would take care of _everything_. Run once and done.

TABLE HERE WHICH LINKS TO VARIOUS SCRIPTS

# Simple Overview for ALL platforms

The easiest thing to do is just get the latest stable release by using `pip install hypatia_engine`.

To install from the GitHub repo:

  1. `git clone https://github.com/lillian-lemmer/hypatia.git`
  2. `cd hypatia`

I recommend you `git checkout develop` to switch to the develop branch. Pull requests branch from `develop`.

Now the next step depends on your Python version:

  3. *Python 3*: `pip install -r requirements/base.txt .`
  3. *Python 2*: `pip install -r requirements/python2.txt .`

If you want to test the source please use (in addition to above):

  4. `pip install -r requirements/testing.txt`

Oh, and don't forget you'll need to manually install `pygame`, so checkout these platform-specific installation notes:

  * [[Installing Hypatia on FreeBSD|Installation-FreeBSD]]
  * [[Installing Hypatia on OpenBSD|Installation-OpenBSD]]
  * [[Installing Hypatia on Ubuntu|Installation-Ubuntu]]
  * [[Installing Hypatia on Linuxmint|Installation-Linuxmint]]
  * [[Installing Hypatia on Windows|Installation-Windows]]
