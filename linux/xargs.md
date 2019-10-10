# xargs

> **xargs** is a command used to build and execute commands from standard input.

### pattern

```bash
arguments_source | xargs command
```

### Sample xargs commands

```bash
find /path -type f -print | xargs rm
```

parallelize operations with `-P maxprocs`

```bash
find /path -name '*.foo' | xargs -P 24 -I '{}' /cpu/bound/process '{}' -o '{}'.out

```

-I option: string replace

```bash
find /path -type f -name '*~' -print0 | xargs -0 -I % cp -a % ~/backups
```
