# Closure Example

> From frontendmaster, good parts of javascript and the web

### global variable version

```javascript
var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];

var digit_name = function (n) {
  return names[n];
}
```

### slow version

```javascript
var digit_name = function () {
  var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
  return names[n];
}
```

### closure version

```javascript
var digit_name = (function () {
  var names = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];

  return function (n) {
    return names[n];
  };
}());
```
