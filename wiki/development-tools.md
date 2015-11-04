---
title: Development Tools
---

Here are the tools I (Lillian) use while developing Hypatia:

  * VIM
  * GIMP
  * ASCIIDoc

## Python Tools

### Cheat Sheets

- **PDF:** [Python 3 Cheat Sheet](https://perso.limsi.fr/pointal/_media/python:cours:mementopython3-english.pdf)

### Pyflakes

[Pyflakes](https://pypi.python.org/pypi/pyflakes) is a linter for Python which helps catch errors and warnings while programming, e.g. unused imports, instead of having to wait and run the application to see such problems appear.  It is also useful in conjunction with [flake8](https://pypi.python.org/pypi/flake8) to catch stylistic problems, i.e. those which do not conform to [PEP 8](https://www.python.org/dev/peps/pep-0008/).

Also see: https://en.m.wikipedia.org/wiki/Lint_(software)

#### GNU Emacs

Developers using [GNU Emacs](https://www.gnu.org/software/emacs/) can install [Flycheck](http://www.flycheck.org/) for real-time syntax checking when writing Python.  Developers using Pyflakes can also use the [flycheck-pyflakes](https://github.com/Wilfred/flycheck-pyflakes) extension, which adds Pyflakes to the list of software Flycheck can use for detecting mistakes when writing Python code.
