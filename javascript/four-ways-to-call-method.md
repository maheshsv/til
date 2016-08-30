# Four ways to call method in JavaScript

### Method form:

- `thisObject.methodName(arguments)`
- `thisObject[methodName](arguments)`

`this` is set to `thisObject`.

### Function form:

- `functionObject(arguments)`

`this` is set to global object.

### Constructor form

- `new FunctionValue(arguments)`

A new object is created and assigned to this.

### Apply form

- `functionObject.apply(thisObject, arguments)`
- `functionObject.call(thisObject, argument...)`

Calling the function, explicitly specifying `thisObject`.
