# 8 super heroic Linux commands

8 super heroic Linux commands introduced in [Engineer Man Video](https://www.youtube.com/watch?v=Zuwa8zlfXSY).

1. redo last command with sudo

```bash
sudo !!
```

2. open an editor to run a command

```bash
ctrl+x+e
```

3. create a super fast ram disk

```bash
mkdir -p /mnt/ram
```

4. don't add command to history

```bash
 ls -l # leading space
```

5. fix a long command you messed up

```bash
fc
```

6. tunnel with ssh (local port 3337 -> remote host's 127.0.0.1 on port 6379)

```bash
ssh -L 3337:127.0.0.1:6379 root@emkc.org -N
```

7. quickly create folders

```bash
mkdir -p folder/{sub1,sub2}/{sub1,sub2,sub3}
mkdir -p folder/{1..100}/{1..100}
```

8. intercept stdout and log to file

```bash
cat file | tee -a log | cat > /dev/null
```

bonus: exit terminal but leave all processes running

```bash
disown -a && exit
```

Really cool commands! I knew some of them before, such as ssh tunnel, mkdir -p and tee, but didn't exploit the full power of these commands.
