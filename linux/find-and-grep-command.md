# find and grep command

## find: walk a file hierarchy, search files.

#### common pattern: `find [path...] [expression]`.

#### common options
* -name
* -perm
* -size
* -mtime
* -type

#### examples:
* find /etc -type d –print
* find . ! -type d –print
* find . -size +1000000c –print

### find and xargs

#### example:
* find . -type f -print | xargs grep "hostname"
* find ./ -mtime +3 -print|xargs rm -f –r

## grep: global search regular expression and print out the line.

#### common patterns: `grep [OPTIONS] PATTERN [FILE...]`, `grep [OPTIONS] [-e PATTERN | -f FILE] [FILE...]`.
