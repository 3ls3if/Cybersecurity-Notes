# 23 - Telnet

## Theory

Telnet is an old way to connect to a remote host using the TCP protocol on port 23 to manipulate the host using the command line (like SSH). Unlike SSH, Telnet communication is not secure, and it's transmitted in cleartext. This protocol was commonly used in legacy networking devices and in Windows operating systems as well. These days we rarely see this protocol enabled in companies, but it's there, and the administrator of the server can enable it whenever they want.

These are the common weaknesses in Telnet:

* Login credentials are sent in cleartext.
* Command‐line text is not encrypted.

### Exploitation Scenarios for Telnet Server

* Credentials brute‐force
* Sniffing for cleartext credentials
* Sniffing for unencrypted command lines
* Finding a public exploit associated with the target Telnet server version

### Enumeration Workflow

* Basic service scan using Nmap
* Advanced scripting scan using Nmap
* Brute‐forcing credentials using Hydra



***

## Practical

### Service Scan

```
nmap ‐sV ‐O ‐sC ‐p23 ‐T5 <IP>
```

### NSE  Scan

```
nmap ‐sV ‐O ‐‐script=telnet* ‐p23 ‐T5 <IP>
```

### Brute Force

#### Hydra

```
hydra ‐t 10 ‐e nsr ‐L <User List> ‐P <Password List> telnet://<IP>
```



***

## REFERENCES

* [https://en.wikipedia.org/wiki/Telnet](https://en.wikipedia.org/wiki/Telnet)
* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-telnet](https://book.hacktricks.xyz/network-services-pentesting/pentesting-telnet)
* [https://www.hackingarticles.in/penetration-testing-telnet-port-23/](https://www.hackingarticles.in/penetration-testing-telnet-port-23/)
* [https://fareedfauzi.gitbook.io/oscp-playbook/services-enumeration/telnet](https://fareedfauzi.gitbook.io/oscp-playbook/services-enumeration/telnet)
