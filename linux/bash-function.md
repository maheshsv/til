# Bash function

Create shortcut with bash function:

```bash
# goto go repo in $GOPATH/src dir
goto() { cd "${GOPATH}/src/$1" }

goto hello # cd $GOPATH/src/hello
```

Implement simple database, from [Designing Data-Intensive Applications](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321).

```bash
#!/bin/bash

db_set() {
  echo "$1,$2" >> database
}

db_get() {
  grep "$1," database | sed -e "s/^$1,//" | tail -n 1
}
```

