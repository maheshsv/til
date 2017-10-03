# JSON Schema

> JSON Schema is a vocabulary that allows you to annotate and validate JSON documents.

[jsonschema](https://github.com/Julian/jsonschema) is an implementation of JSON Schema for Python.

```pyth
>>> from jsonschema import validate

>>> # A sample schema, like what we'd get from json.load()
>>> schema = {
...     "type" : "object",
...     "properties" : {
...         "price" : {"type" : "number"},
...         "name" : {"type" : "string", "minLength": 2, "maxLength": 20},
...     },
... }

>>> # If no exception is raised by validate(), the instance is valid.
>>> validate({"name" : "Eggs", "price" : 34.99}, schema)
```

JSON Schema validation keywords can be found [here](http://json-schema.org/latest/json-schema-validation.html).

### Validate `date-time` format using Python jsonschema

```python
# strict-rfc3339 package should be installed.
jsonschema.validate(data, schema, format_checker=jsonschema.FormatChecker())
```

