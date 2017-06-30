# Python Logging Architecture

### The components of Python logging system:

- **filter**: provide a finer grained facility for determining which log records to output
- **handler**: send the log records (created by loggers) to the appropriate destination
- **formatter**: specify the layout of log records in the final output
- **logger**: expose the interface that application code directly uses

The logging flow:
![logging flow](https://docs.python.org/3.5/_images/logging_flow.png)

<sup>[Python Logging](https://docs.python.org/3.5/howto/logging.html#logging-advanced-tutorial)</sup>
