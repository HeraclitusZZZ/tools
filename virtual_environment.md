# Virtual Environment

Virtual environments are used to create and manage separate environments for your Python projects, each using different versions of Python for execution.

## Why the Need for Virtual Environments?

There are a few different locations where these packages can be installed on your system. For example, most system packages are stored in a child directory of the path stored in sys.prefix.

On Mac OS X, you can easily find where `sys.prefix` points to using the Python shell:

```python
import sys
sys.prefix
```

Third party packages installed using `easy_install` or `pip` are typically placed in one of the directories pointed to by `site.getsitepackages`:

```python
import site
site.getsitepackages()
```

It’s important to know this because, by default, every project on your system will use these same directories to store and retrieve **site packages** (third party libraries). At first glance, this may not seem like a big deal, and it isn’t really, for **system packages** (packages that are part of the standard Python library), but it does matter for **site packages**.

Consider the following scenario where you have two projects: *ProjectA* and *ProjectB*, both of which have a dependency on the same library, *ProjectC*. The problem becomes apparent when we start requiring different versions of *ProjectC*. Maybe *ProjectA* needs v1.0.0, while *ProjectB* requires the newer v2.0.0, for example.

Since projects are stored according to just their name, there is no differentiation between versions. Thus, both projects, *ProjectA* and *ProjectB*, would be required to use the same version, which is unacceptable in many cases.

This is where virtual environments and the `virtualenv`/`venv` tools come into play.

## What Is a Virtual Environment?

At its core, the main purpose of Python virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has.

In our little example above, we’d just need to create a separate virtual environment for both *ProjectA* and *ProjectB*, and we’d be good to go. Each environment, in turn, would be able to depend on whatever version of *ProjectC* they choose, independent of the other.

The great thing about this is that there are no limits to the number of environments you can have since they’re just directories containing a few scripts. Plus, they’re easily created using the `virtualenv` or `pyenv` command line tools.

## Using Virtual Environments

To get started, if you’re not using Python 3, you’ll want to install the `virtualenv` tool with pip:

```console
pip install virtualenv
```

If you are using Python 3, then you should already have the `venv` module from the standard library installed.

Start by making a new directory to work with:

```console
mkdir python-virtual-environments && cd python-virtual-environments
```

Create a new virtual environment inside the directory:

```console
python3 -m venv env
```





