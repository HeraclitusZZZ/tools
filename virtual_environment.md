# Virtual Environment

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
