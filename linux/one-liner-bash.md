# One Liner Bash

> Notes from a colleague's tech talk.

## Useful Tools

- AWK: string tranformation program at the line level
    - Usage: `awk 'BEGIN{X} condition{Y} END{Z}'`

### Question 1: Word Frequency

```
$ cat file.txt | tr -s [:space:] '\n' | tr [:upper:] [:lower:] | tr -d [:punct:] | sort | uniq -c
```

### Question 2: Rot 13 encryption

```
$ cat file.txt | tr A-Za-z N-ZA-Mn-za-m | tee encrypted.txt | head -10
```

### Question 3: 10 largest files in a given directory

```
$ find /dir/ -type f | xargs -Ipath du path | sort -nr | head -10
```

### Question 4: Batch renaming

```
$ find . -name '*.txt' -type f -maxdepth 1 | xargs -Ifilename ls -nl filename | awk '{print "mv "$9" "$9"."$5".bak"}' | sh
```

### Question 5: Memory hoggers

```
$ ps aux | awk '$4 > 1 {print $2}' | xargs -Ipid ps -p pid -o comm | grep -v COMM | xargs -Ipath du path | sort -n
```

### Question 6: Overworked python

```
$ find apps -name *.py | xargs awk '{print FILENAME, $0}' | egrep '^[^#]+ class \w+(\(\w+\))?:' | cut -d ' ' -f1 | uniq -c | awk '$1 > 1 {print $2}'
```

### Question 7: Hot files

```
$ git log --pretty=format: --name-only | tr -s [:space:] '\n' | sort | uniq -c | sort -r | head -5 | awk '{x="git log --pretty=format:\"%an %H\" -n 1 "$2; x | getline y; close(x); print $2, y}'
```
