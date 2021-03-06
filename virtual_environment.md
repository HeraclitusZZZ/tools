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

In the above example, this command creates a directory called `env`, which contains a directory structure similar to this:

```console
placeholder
```

Here’s what each folder contains:

- bin: files that interact with the virtual environment
- include: C headers that compile the Python packages
- lib: a copy of the Python version along with a `site-packages` folder where each dependency is installed

Further, there are copies of, or `symlinks` to, a few different Python tools as well as to the Python executables themselves. These files are used to ensure that all Python code and commands are executed within the context of the current environment, which is how the isolation from the global environment is achieved. We’ll explain this in more detail in the next section.

More interesting are the **activate scripts** in the bin directory. These scripts are used to set up your shell to use the environment’s Python executable and its `site-packages` by default.

In order to use this environment’s packages/resources in isolation, you need to `activate` it. To do this, just run the following:

```console
source env/bin/activate
```

Notice how your prompt is now prefixed with the name of your environment (env, in our case). This is the indicator that env is currently active, which means the python executable will only use this environment’s packages and settings.

We can go back to the `system` context by executing deactivate:

```console
deactivate
```

Now your shell session is back to normal, and the python command refers to the global Python install. Remember to do this whenever you’re done using a specific virtual environment.

## How Does a Virtual Environment Work?

What exactly does it mean to `activate` an environment? Knowing what’s going on under the hood can be pretty important for a developer, especially when you need to understand execution environments, dependency resolution, and so on.

To explain how this works, let’s first check out the locations of the different python executables. With the environment `deactivated`, run the following:

```console
which python
```

Now, `activate` it and run the command again:

```console
source env/bin/activate
which python
```

After activating the environment, we’re now getting a different path for the python executable because, in an active environment, the `$PATH` environment variable is slightly modified.

Notice the difference between the first path in `$PATH` before and after the activation:

```console
echo $PATH

source env/bin/activate
echo $PATH
```

In the latter example, our virtual environment’s `bin` directory is now at the beginning of the path. That means it’s the first directory searched when running an executable on the command line. Thus, the shell uses our virtual environment’s instance of Python instead of the system-wide version.

Only directory locations matter.

When Python is starting up, it looks at the path of its binary. In a virtual environment, it is actually just a copy of, or symlink to, your system’s Python binary. It then sets the location of `sys.prefix` and `sys.exec_prefix` based on this location, omitting the `bin` portion of the path.

The path located in `sys.prefix` is then used for locating the `site-packages` directory by searching the relative path `lib/pythonX.X/site-packages/`, where X.X is the version of Python you’re using.

## Managing Virtual Environment with Anaconda

With conda, you can create, export, list, remove, and update environments that have different versions of Python and/or packages installed in them. Switching or moving between environments is called activating the environment. You can also share an environment file.

By default, environments are installed into the `envs` directory in your conda directory. Run `conda create --help` for information on specifying a different path.

1. Use the terminal or an Anaconda Prompt for the following steps:

```console
conda create --name myenv
```

Replace `myenv` with the environment name.

2. When conda asks you to proceed, type `y`:

```console
proceed ([y]/n)?
```

This creates the myenv environment in `/envs/`. No packages will be installed in this environment.

3. To create an environment with a specific version of Python:

```console
conda create -n myenv python=3.6
```

4. To create an environment with a specific package:

```console
conda create -n myenv scipy
```

or

```console
conda create -n myenv python
conda install -n myenv scipy
```

5. To create an environment with a specific version of a package:

```console
conda create -n myenv scipy=0.15.0
```

or

```console
conda create -n myenv python
conda install -n myenv scipy=0.15.0
```

6. To create an environment with a specific version of Python and multiple packages:

```console
conda create -n myenv python=3.6 scipy=0.15.0 astroid babel
```

To automatically install pip or another program every time a new environment is created, add the default programs to the create_default_packages section of your `.condarc` configuration file. The default packages are installed every time you create a new environment. If you do not want the default packages installed in a particular environment, use the `--no-default-packages` flag:

```console
conda create --no-default-packages -n myenv python
```

## Creating an environment from an environment.yml file

Use the terminal or an Anaconda Prompt for the following steps:

1. Create the environment from the `environment.yml` file:

```console
conda env create -f environment.yml
```

The first line of the `yml` file sets the new environment's name.

2. Activate the new environment: `conda activate myenv`

3. Verify that the new environment was installed correctly:

```console
conda env list
```

You can also use `conda info --envs`.

## Activating an Environment

Activating environments is essential to making the software in the environments work well. Activation entails two primary functions: adding entries to PATH for the environment and running any activation scripts that the environment may contain. These activation scripts are how packages can set arbitrary environment variables that may be necessary for their operation.

When installing Anaconda, you have the option to “Add Anaconda to my PATH environment variable.” This is not recommended because the add to PATH option appends Anaconda to PATH. When the installer appends to PATH, it does not call the activation scripts.

Activation prepends to `PATH`. This only takes effect when you have the environment active so it is local to a terminal session, not global.

To activate an environment: `conda activate myenv`
