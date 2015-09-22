## Purpose

This document denotes, primarily, guidelines for developers when contributing to Hypatia. Although, this also serves as a general contributors guideline document.

If you're looking for the _code of conduct_, there is a +code-of-conduct.adoc+ file in the project root.

## Pull Requests

I (try to) use this git branching model: [A Successful git Branching Model](http://nvie.com/posts/a-successful-git-branching-model/). Please branch from the `develop` branch.

## Marketing, Branding

  * The official brand color of Hypatia is `#333333`
  * Use the brand color whenever possible
  * Use the official logos, icons whenever possible from [master tree `media/` directory](https://github.com/lillian-lemmer/hypatia/tree/master/media)

## Documents, Documentation

### Rules

  * Always use gender neutral pronouns in all documentation, including code comments, e.g., they, them, their.
  * Use one space (not two) to separate sentence.
  * Docstrings are in reStructuredText, documents are markdown (wiki, readme, etc.)

### An idea of what documentation entails:

  * Lots of tutorials
    * Tutorials for creatives
    * Tutorials for developers


  * Lots of media, especially recordings, showing off the engine, tutorials, etc.
    * YouTube videos
    * GIFs, webm
    * Screenshots


  * All document source in ASCIIDoc
    * Wiki
    * Readme documents
    * Website

## Python Style Guidelines

Hypatia is strict about the style of code.

  * Aim for 100% test coverage, as seen through [coveralls.io](https://coveralls.io/r/lillian-lemmer/hypatia)
  * Hypatia has a strict style code. PEP8 nonconforming code will generate errors on the [Travis CI account](https://travis-ci.org/lillian-lemmer/hypatia)
  * Code is also checked by [code climate](https://codeclimate.com/github/lillian-lemmer/hypatia)
  * Use `test.sh` in the repo's root to test your code *before* commit. It uses `pytest`, `pytest-cov`, and `pytest-pep8`.

### My particular style

The following statements must have a blank line above and below:

  * `return`
  * `break`
  * `continue`
  * `yield`
  * `raise`

Examples of what _must have a blank line above and below_:

```
if x == 2:

    continue

elif x == 3:

    return None

elif x == 4:
    x += 1
elif x == 6:

    break

elif x == 10:

    raise Exception('derp!')
```

The following must have a blank line above:

  * `except`: when the respective `try` block exceeds one line
  * `else`, `elif`: when the previous `else`, `elif`, or `if` block exceeded one line

Example of what _must have a blank line above_:

```
try:
    d = {}
    d['lol no such key']

except KeyError:
    print("what a horrible example")

if x == 3:
    x += 5
    y -= 3
    a = x - y

elif x == 5:
    x -= 4
elif x == 6:
    x += 8
    y -= 9

else:
    x = 5
```

I tend to favor this method for writing long lists:

```
a_long_list # [
               'i guess this list was too long',
               'so it got broken up into chunks',
               'and I decided to format it like this',
               'which is what i've seen in pep8'
              ]
```

### Docstrings

Hypatia is strictest about _docstrings_. The docstring convention used is the Google docstring format. Here are some great references on that style:

  * [Example Google docstrings](http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_google.html)
  * [The official spec from Google](http://google.github.io/styleguide/pyguide.html)
  * Use FOUR spaces to indent things in docstrings, NOT two!
  * We use Sphinx to generate our API docs, for more info see `sphinx-source/readme.asciidoc`.
  * Napoleon is a Sphinx module we use which parses Google-style docstrings. It'd be a good idea to read [the official Napoleon/Google docstring docs](http://sphinxcontrib-napoleon.readthedocs.org/en/latest/).
  * [Fancier usage example](http://gki.informatik.uni-freiburg.de/teaching/ws1415/info1/docs/example.py)
  * Don't go crazy with restfultext markdown

Docstrings are required for modules, functions, classes, and methods.

#### Doctests

We also use require doctests for all classes, methods, and functions. It is also required to run doctest if a module is being executed as main. Here are some relevant cherry-picked resources on the matter:

  * [Official Python guide on doctests](https://docs.python.org/2/library/doctest.html)
  * [A wonderful, more thorough guide on doctests](http://pymotw.com/2/doctest/)

Our doctests are verified by Travis CI. You can avoid embarassment by running the `test.sh` supplied in the repo to test your changes.

## Testing/py.test/tests

The `test.sh` should be sufficient. Ensure that py.test is in your $PATH for `test.sh` to run properly.

### Creating tests
* Hypatia uses pytest for automated testing. See the [[Installation-Instructions|Installation-Instructions]] on how to setup your install for testing
* Reference `tests/test_tiles.py` for an example on how to structure your tests. See [official pytest usage examples](http://pytest.org/latest/example) for more generic samples. 
    * avoid creating classes in your tests
    * The following try/except block is needed:
```
    try:
        os.chdir('demo')
    except OSError:
        pass
```