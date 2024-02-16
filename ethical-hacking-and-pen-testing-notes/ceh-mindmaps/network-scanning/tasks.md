# Tasks

## Host Discovery



Perform an ICMP ECHO ping sweep to discover live hosts on your network subnet. Find the number of live hosts in the subnet (10.10.1.2-23).

```
nmap -sn -PE <IP range>
```



Perform host discovery using Nmap and find the IP address of the machine hosting [www.moviescope.com](http://www.moviescope.com).

```
nmap -sn www.moviescope.com
```





## Port and Service Discovery



### MegaPing

* Install
* IP Scanner
* Port Scanner



Perform port and service discovery using MegaPing and name the service running on port 445 on the Windows Server 2022 machine.

Microsoft-DS



Perform port and service discovery using MegaPing and find the IP address of the machine with an open FTP port.

10.10.1.11



Perform port and service discovery using MegaPing and find the IP address of the machine with an open SSH port.

10.10.1.9



### NetScanTools Pro



Perform port and service discovery using NetScanTools Pro and identify the port used by the epmap service.

135



### SX Tool



Use sx tool to perform ARP scans, TCP scans and UDP scans to discover open ports in the Windows 11 machine. Enter the option that specifies the target port while performing a UDP scan.

```
sx arp <ip/cidr>
```

```
sx arp <target subnet> --json | tee arp.cache
```

```
cat arp.cache | sx udp --json -p <port number> <IP addr>
```

```
cat arp.cache | sx tcp --json -p <port number> <IP addr>
```



### Nmap

Use Nmap to perform a TCP connect/full open scan and find the port number used by the ldapssl service on the Windows Server 2022 machine.

```
nmap -sT -v <IP address>
```

sT: TCP Connect/full open scan

\-v: enables the verbose output



Use Nmap to perform a Null scan with the timing template set to Aggressive (-T4) and all advanced/aggressive options (-A) enabled. Find the version of the Apache service running on port 80 on the machine at 10.10.1.9

```
nmap -sN -T4 -A -v 10.10.1.9
```



### Hping3

Use the Hping3 tool to discover open ports and services running on the Windows Server 2022 machine. Enter the port number of the “systat” service running on the Windows Server 2022 machine.

```
hping3 -8 0-100 -S <IP address> -V
```

\-8: Specifies Scan Mode

\-p: Specifies range of ports (0-100)

\-V: Specifies verbose mode





## OS Discovery

### Nmap Script Engine (NSE)

Use Nmap Scripting Engine (NSE) to perform OS discovery and find the OS on the machine at the IP address 10.10.1.22.

```
nmap -A <IP address>
```

```
nmap -O <IP address>
```

```
nmap --script smb-os-discovery.nse <IP address>
```



## Scan Beyond IDS and Firewall

### Nmap

Use the Nmap tool to scan beyond the IDS/firewall of the target machine (Windows 11). Enter the Nmap option, which is used to split the IP packet into tiny fragment packets. Note: Turn on the Windows Firewall to perform this task.

```
nmap -f <IP address>
```



### Colasoft Packet Builder

In Windows Server 2019, use the Colasoft Packet Builder tool to create custom packets to scan the target host (Windows 11). Observe the “Decode Editor” section and find out the packet length value. Note: Turn on the Windows Defender Firewall to perform this task.

64



### Hping3

Use the Hping3 tool to create custom UDP and TCP packets to evade the IDS/firewall of the target machine (Windows 11). Enter the option which performs TCP flooding. Note: Turn on the Windows Defender Firewall to perform this task.

```
hping3 <IP address> --flood
```





## Network Scanning using Various Tools

### Metasploit

Use the Metasploit to scan the target machine. While using Metasploit auxiliary module “auxiliary/scanner/smb/smb\_version”, enter the specified range of remote hosts (RHOSTS).

10.10.1.5-23

