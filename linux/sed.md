# sed

sed: stream editor.

The basic usage:

```bash
sed [options] commands [file-to-edit]
```

Replace all old word with new word in a file.

```bash
sed -i -e 's/old_word/new_word/g' file.txt
```

