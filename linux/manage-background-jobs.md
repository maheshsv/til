# Manage background jobs with: jobs, Ctrl-z, bg, fg, &

1. &: execute a job in the background.

```
$ python manage.py runserver &
```

2. Ctrl-z: send a running job to the background.

```
# python manage.py runserver

^Z
[1]  + 47845 suspended  python manage.py runserver
```

3. jobs: list background jobs

```
$ jobs
[1]  + suspended  python manage.py runserver
```

4. bg: resume suspended jobs while keeping them running in the background

```
$ bg
$ jobs
[1]  + running    python manage.py runserver
```

5. fg: take a background job to the foreground

```
$ fg
[1]  + 47845 running    python manage.py runserver
```
