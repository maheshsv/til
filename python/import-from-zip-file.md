# Import from zip file

Python supports [importing modules from ZIP archive](https://docs.python.org/2/library/zipimport.html). Here is an example.

1. create a example.py file with content like:

```python
def foo():
    print("bar")
```

2. create zip archive with `zip example.zip example.py`, assume the file is in /tmp.

3. in another directory, run python REPL:

```shell
>>> import sys
>>> from example import *
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'example'
>>>
>>> sys.path.append("/tmp/example.zip")
>>>
>>> from example import *
>>>
>>> foo()
bar
```

when `example.zip` is added to sys.path, we can import module from it.
