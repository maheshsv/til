# Python Virtualenv and Virtualenvwrapper

[Virtualenv](https://virtualenv.readthedocs.org/en/latest/) is a tool to create isolated Python environments.

The basic command is:

```bash
$ virtualenv ENV
```

`ENV` is the directory to place the new environment, supporting libraries/packages, a new **Python**, `pip` and so on.

To activate the environment:

```bash
cd ENV
$ source bin/activaate # basically execute this bash script.
```

To exit from the environment:

```bash
$ deactivate
```

To remove the environment:

```bash
$ rm -r /path/to/ENV
```

[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) is a set of extensions to Virtualenv. It organizes and manages all of the virtual environment in one place.

The command to create a new environment:

```bash
$ mkvirtualenv env1
```

To activate and switch to different environment:

```bash
$ workon env1
```
