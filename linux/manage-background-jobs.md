# Manage background jobs with: jobs, Ctrl-z, bg, fg, &

**&**: execute a job in the background.

```
$ python manage.py runserver &
```

**Ctrl-z**: send a running job to the background.

```
# python manage.py runserver

^Z
[1]  + 47845 suspended  python manage.py runserver
```

**jobs**: list background jobs

```
$ jobs
[1]  + suspended  python manage.py runserver
```

**bg**: resume suspended jobs while keeping them running in the background

```
$ bg
$ jobs
[1]  + running    python manage.py runserver
```

**fg**: take a background job to the foreground

```
$ fg
[1]  + 47845 running    python manage.py runserver
```
