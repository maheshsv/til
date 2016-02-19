# Create remote git branch

The steps to create a remote git branch:

1. create a local branch

```
git branch my-branch
```

2. push `my-branch` to remote

```
git push -u origin my-branch
```

The steps other people can get `my-branch`:

```
git fetch
git checkout origin/my-branch
```
