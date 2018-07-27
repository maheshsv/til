# Awk

>  Awk - pattern-directed scanning and processing language.



`awk '{print $0}'`: most Awk programs start with a "{" and end with a "}", everything in between there gets run once on each line of the input.

`$0` is the entire line, whitespace(space, tab) are delimiter, the fields are the variables:`$1, $2...`.

examples:

```bash
echo 'this is a test' | awk '{print $3}'
awk '{print $1}' logs.txt
```

Special variable `NF`: number of fields in the current line.

```bash
	echo 'this is a test' | awk '{print $NF}' // prints "test"
	echo 'this is a test' | awk '{print $(NF - 1)}' // prints second to the last field
	awk '{print $1, $(NF - 2)}' logs.txt
```

Special variable `NR`current row number.

```bash
awk '{print NR ") " $1 " -> " $(NF-2)}' logs.txt
```

Field seperator: `fs`

```bash
echo '2018/07/26' | awk 'BEGIN{FS="/"}{print $1}' // prints 2018
awk '{print $2}' logs.txt | awk 'BEGIN{FS=":"}{print $1}' | sed 's/\[//'
```

`if` logic

```bash
awk '{if ($(NF - 2) == "200") {print $0}}' logs.txt
```

Sum up:

```bash
awk '{a+=$(NF-2); print "Total so far: ", a}' logs.txt
```

`END` clause:

```bash
awk '{a+=$(NF-2)}END{print "Total: ", a}' logs.txt
```



Notes from [learn just a little Awk](https://gregable.com/2010/09/why-you-should-know-just-little-awk.html).

