# 21 - FTP

## Theory

The File Transfer Protocol (FTP) is used to transfer files between a client and a remote server. The latter is used to stock files so you can access them remotely. Sometimes FTP is used by web applications to synchronize the hosted source code (e.g., HTML, JavaScript, etc.). Two secure implementations of FTP are FTPS and SFTP. Secure File Transfer Protocol (SFTP) uses the SSH protocol to transmit files (by default, it uses the same port 22 of SSH). On the other hand, the File Transfer Protocol Secure (FTPS) uses SSL to encrypt the file transfer, and it uses ports 989 and 990 for this purpose.

These are the common weaknesses in the FTP protocol:

* Login credentials are sent in clear-text.&#x20;
* File transmission is not encrypted.

### Exploitation Scenarios

* Credentials brute‐force&#x20;
* Sniffing for clear-text credentials&#x20;
* Sniffing for unencrypted files&#x20;
* Anonymous access&#x20;
* Finding a public exploit associated with the target FTP server version



***

## Practical

### Service Scan

```
nmap ‐sV ‐O ‐sC ‐p21 ‐T5 <IP>
```

### Advanced Scripting Scan with Nmap

```
nmap ‐sV ‐O ‐‐script=ftp* ‐p21 ‐T5 <IP>
```

### Brute Forcing

#### Hydra

```
hydra ‐t 10 ‐L <Username List> ‐P <Password List> ftp://<IP>
```

* **-t 10** : Run with 10 parallel threads
* **-L** : Path to the users file
* **-P** : Path to the passwords file



***

## REFERENCES

* [https://en.wikipedia.org/wiki/File\_Transfer\_Protocol](https://en.wikipedia.org/wiki/File\_Transfer\_Protocol)
* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-ftp](https://book.hacktricks.xyz/network-services-pentesting/pentesting-ftp)
* [https://0xffsec.com/handbook/services/ftp/](https://0xffsec.com/handbook/services/ftp/)
* [https://pentestmonkey.net/tools/user-enumeration/ftp-user-enum](https://pentestmonkey.net/tools/user-enumeration/ftp-user-enum)
