# date, datetime, string convertion in Python

### Convert from string such as `2016-02-10` to datetime object:

```python
> from datetime import datetime
> datetime.strptime('2016-01-10', '%Y-%m-%d')
datetime.datetime(2016, 1, 10, 0, 0)
```

### String format datetime object:

```python
> datetime.now().strftime("%A, %d. %B %Y %I:%M%p")
'Wednesday, 24. February 2015 07:53PM'
```

Format list:

| Directive     | Meaning       |
| ------------- | ------------- |
| %Y            | Year with century as a decimal number.  |
| %m            | Month as a zero-padded decimal number.  |
| %d            | Day of the month as a zero-padded decimal number. |
| %H            | Hour (24-hour clock) as a zero-padded decimal number. |
| %M            | Minute as a zero-padded decimal number. |
| %S            | Second as a zero-padded decimal number. |

The complete list can be found [here](https://docs.python.org/2/library/datetime.html).

### Conver from date to datetime object and from datetime to date object:

```python
> from datetime import date
> from datetime import datetime
> d = date.today()
> datetime.combine(d, datetime.min.time())
datetime.datetime(2016, 2, 10, 0, 0)

> datetime.now().date()
datetime.date(2016, 2, 10)
```
