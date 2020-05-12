# example-python-project
Example structure for a python project with make-based CI targets


# How to use

## Requirements and virtual environment

By default, this repo is setup to use Python 3 for all development.  Unless there's a very good reason, all new projects should target Python 3 as their primary platform.

Best practice is to list all of your project requirements in the file `requirements.txt`.  This file can then be used in conjunction with `pip` to create virtual environments (virtualenvs), allowing you to install dependencies
locally without touching your system Python libraries.

The `Makefile` is setup to use `requirements.txt` and `test-requirements.txt` to create a self-contained Python virtualenv called `venv_myproject` located in the base directory.  Should you wish to also use this virtualenv while developing, you can simply run: 
```
source venv_myproject/bin/activate
```

## Makefile targets

A number of default make targets are provided.  You can run `make help` to get a short summary of each.

Useful targets:
  * `make check`: runs `yapf` and `pylint` to check formatting and code correctness.  A `.pylintrc` is  provided with some defaults to make it a little less picky.
  * `make docs` : build documentation in HTML and Markdown.  By default, it will automatically generate API documentation for everyting in `myproject`.  Output documents can be found in `docs/build`.
  * `make clean`: cleans up generated binaries, virtualenvs, and documentation


## Auto-generated documentation

With proper docstrings, this repo can be used to automatically generate SDK/API documentation in a variety of formats.  It uses [Sphinx](https://www.sphinx-doc.org/en/master/),  and [sphinx-autoapi](https://sphinx-autoapi.readthedocs.io/en/latest/) to parse `autoapi_dirs` given in `docs/source/conf.py`.   Some example docstrings are provided in `myproject/mymodule.py`.

## CI/CD

### TravisCI
A brief configuration for [TravisCI](https://travis-ci.com) is provided in `.travis.yml`.  For external GitHub repos, Travis provides a quick and easy way to test your code against multiple Python version.  For more information on getting Travis setup, please reach out to the DevOps team.

### Jenkins
A minimal [Jenkins](https://www.jenkins.io) configuration is provided in the `Jenkinsfile`.  For project that are location on internal Github, or project that require secret credentials to run their tests, Jenkins may be a better choice than Travis.  

## CLI
Also included is a very brief example of how to use [Click](https://click.palletsprojects.com/) to quickly construct a CLI for your project.  Click is a widely used library for Python CLI utilities, and is much better than writing your own command line parser.  To test it out, you could do:
```
make deps                          # initialize your virtualenv
source venv_myproject/bin/activate # activate the venv
pip install -e .                   # "install" the project to create the CLI executable
rehash                             # update list of executables in your path in some shells
myproject-cli --help               # run the thing
```