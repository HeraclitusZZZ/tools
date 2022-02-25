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
