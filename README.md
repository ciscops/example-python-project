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
  * `make check` - runs `yapf` and `pylint` to check formatting and code correctness.  A `.pylintrc` is  provided with some defaults to make it a little less picky.
  * `make docs` will build documentation in HTML and Markdown.  By default, it will automatically generate API documentation for everyting in `myproject`.  Output documents can be found in `docs/build`.

