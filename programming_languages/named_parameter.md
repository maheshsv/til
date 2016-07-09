# Named parameter

From [wikipedia]: In computer programming, named parameters, pass-by-name, or keyword arguments refer to a computer language's support for function calls that clearly state the name of each parameter within the function call.

### Optional and Named arguments in Python [example](http://www.diveintopython.net/power_of_introspection/optional_arguments.html):

```python
def info(object, spacing=10, collapse=1):
    pass
```

Valid calls of `info`:

```python
info(odbchelper)
info(odbchelper, 12)
info(odbchelper, collapse=0)
info(spacing=15, object=odbchelper)
```

`info(odbchelper)` with only one argument, `spacing` default to 10, `collapse` default to 1
`info(odbchelper, 12)`, with two arguments, `spacing` is 12, `collapse` default to 1
`info(odbchelper, collapse=0)` with two arguments, `spacing` default to 10, `collapse` is 0
`info(spacing=15, object=odbchelper)` named arguments can appear in any order
