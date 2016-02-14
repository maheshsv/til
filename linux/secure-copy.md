# Secure copy

**scp**, copy files between different hosts securely.

Copy file 'foo.txt' from local to remote directory:

```bash
scp /path/to/file/foo.txt username@remotehost:/path/to/remote/directory
```

Copy remote host file 'foo.txt' to local:

```bash
scp username@remotehost:/path/to/file/foo.txt /path/to/local/directory
```

Copy local directory to remote host:

```bash
scp -r /path/of/local/directory username@remotehost/path/to/remote/directory
```

Copy more than one files from local to remote host home directory:

```bash
scp foo.txt bar.txt username@remotehost:~
```

Copy remote host directory to current directory:

```bash
scp username@remotehost:/path/to/directory .
```
