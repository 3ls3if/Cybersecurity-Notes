# SSH Tunneling

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

## Create a Tunnel

```
ssh -nNT -f -L 8080:localhost:80 ubuntu@192.168.1.151
```

## Kill the SSH Tunnel

```
ps aux | grep ssh

kill <pid>
```

