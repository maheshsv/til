# Linux: /etc/init.d and service command

`/etc/init.d` is an important dir in Linux and the common way to use it is:

```
$ /etc/init.d/command OPTION(start|stop|restart)
```

And we use `service` command in similar way because service is a wrapper for scripts in `/etc/init.d`.
