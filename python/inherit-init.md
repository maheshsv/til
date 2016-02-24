# Inheritance of __init__ in Python

Considering we have a superclass like:

```python
class Foo():
    def __init__(self):
        self.a = 1
```

Then `Foo().a` is `1`.

And then if we have a subclass:

```python
class Bar(Foo):
    def __init__(self):
        self.b = 2
```

Now if we call `Bar().a`, it will raise `AttributeError: Bar instance has no attribute 'a'`. That's because:

> When a class defines an __init__() method, class instantiation automatically invokes __init__() for the newly-created class instance.

If we want to have both instance variable `a` and `b` in the subclass, we should do:

```python
class Sub(Foo):
    def __init__(self):
        Foo.__init__(self)
        self.b = 2
```

Now `Sub().a` is `1` and `Sub().b` is `2`.
