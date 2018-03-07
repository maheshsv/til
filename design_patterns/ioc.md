# Inversion of Control

IoC, Inversion of Control is a design pattern in extending frameworks. 

A sample **in control** code looks like:

```python
do_something_A()
do_something_B()
do_something_C()
```

Which means you are controling every action, when to call them.

### IoC in a framework

Considering using a web framework, for example: RoR. We can define a controller like:

```ruby
class ClientsController < ApplicationController
    def new
        # create a new client
    end
end
```

In this case we don't call `ClientsController` ourselve. It's called by the framework, that's **Inversion of Control**.

> Inversion of Control is a key part of what makes a framework different to a library.

### IoC approaches

- define event and bind client code with the event.
- define interface/abstract class, client code implement interface/abstract class.

DI, dependency injection is one style of IoC.

A good read of Ioc is [here](https://martinfowler.com/bliki/InversionOfControl.html).

