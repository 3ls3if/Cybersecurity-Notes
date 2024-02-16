# Tasks

## NetBIOS Enumeration

### Windows Command Line Utility

Name the shared folder/drive available on the Windows Server 2019 machine.

\WINDOWS11\CEH-Tools

```
net use
```

### NetBIOS Enumerator

Use the NetBIOS Enumerator to perform NetBIOS enumeration on the network (10.10.1.15 – 10.10.1.100). Enter the domain name associated with the IP address 10.10.1.22.

CEH

### NSE Script

```
nmap -sV -v --script nbstat.nse <IP address>
```



## SNMP Enumeration

### snmp-check

Use snmp-check to enumerate a target and find the hostname of the machine at the IP address 10.10.1.22.

Server2022.CEH.com

```
nmap -sU -p 161 <IP address>
```

```
snmp-check <IP address>
```



What is the domain name of the machine at the IP address 10.10.1.22?

CEH



Enumerate the machine at 10.10.1.22 using snmp-check and find the number of user accounts.

6

### SoftPerfect Network Scanner

Perform SNMP enumeration using SoftPerfect Network Scanner and find the hostname of the machine at 10.10.1.9

ubuntu.local



Perform SNMP enumeration using SoftPerfect Network Scanner and find the hostname of the machine at 10.10.1.14

Android.local



Perform SNMP enumeration using SoftPerfect Network Scanner and find the Host Name of the machine at 10.10.1.22

SERVER2022

### SnmpWalk

Use SnmpWalk to perform SNMP enumeration on the Windows Server 2022 machine. Enter the option that sets a community string.

\-c

```
snmpwalk -v1 -c public <IP address>
```

```
snmpwalk -v2c -c public <IP address>
```

### Nmap

Use various Nmap scripts to perform SNMP enumeration on the Windows Server 2022 machine. What is the option that is used to specify a UDP scan?

\-sU

```
nmap -sU -p 161 --script=snmp-sysdescr <IP address>
```

```
nmap -sU -p 161 --script=snmp-processes <IP address>
```

```
nmap -sU -p 161 --script=snmp-win32-software <IP address>
```

```
nmap -sU -p 161 --script=snmp-interfaces <IP address>
```



Use various Nmap scripts to perform SNMP enumeration on the Windows Server 2022 machine. Enter the option that specifies the port to be scanned.

\-p



## LDAP Enumeration

### Active Directory Explorer

Perform LDAP Enumeration using Active Directory Explorer (AD Explorer) and find the Domain Controller machine's IP address.

10.10.1.22

Perform LDAP enumeration using Active Directory Explorer (AD Explorer) and find the userPrincipalName for the user named Jason.

jason@CEH.com

### Python and Nmap

Use Nmap and Python commands to extract details on the LDAP server and connection. Enter the port number that is used by LDAP.

389

```
nmap -sU -p 389 <IP address>
```

#### Username Enumeration

```
nmap -p 389 --script ldap.brute --script-args ldap.base='"cn=users,dc=CEH,dc=com"' <IP address>
```

#### Using Python3

```
python3

import ldap3

server = ldap3.server('[IP address]', get_info=ldap3.ALL,port=[target port])

connection = ldap3.Connection(server)

connection.bind()

server.info

connection.search(search_base='DC=CEH,DC=COM',search_filter='(&(objectclass=*))',search_scope='SUBTREE',attributes='*')

connection.entries

connection.search(search_base='DC=CEH,DC=com',search_filter='(&(objectclass=person))',search_scope='SUBTREE',attributes='userpassword')

connection.entries
```



Use Python commands to extract details on the LDAP server and connection. Enter the command used in python shell to gather information such as naming context or domain name.

server.info

### ldapsearch

Use ldapsearch to perform LDAP enumeration on the target system to gather details related to the naming contexts. Which option is used to specify simple authentication?

\-x

```
ldapsearch -h <IP address> -x -s base namingcontexts
```

\-h : specifies the host

\-x : specifies simple authentication

\-s : specifies the scope



Use ldapsearch to perform LDAP enumeration on the target system to obtain more information about the primary domain. Which option is used to specify the base DN for search?

\-b

```
ldapsearch -h <IP address> -x -b "DC=CEH,DC=com"
```



## NFS Enumeration

Perform NFS Enumeration using RPCScan and SuperEnum and find the port used by the NFS service on 10.10.1.19.

2049

```
nmap -p 2049 <IP address>
```

### SuperEnum

```
echo "<Target IP address>" >> Target.txt

./superenum

Target.txt
```

### RPCScan

```
python3 rpc-scan.py <IP address> --rpc
```



## DNS Enumeration

### Zone Transfer

Can you perform zone transfer on the primary host of certifiedhacker.com?

No

```
dig ns <Target Domain>
```

```
dig @<Name Server> <Target Domain> axfr
```



Perform DNS enumeration and find the “responsible mail address” for the domain certifiedhacker.com.

dnsadmin.box5331.bluehost.com

```
nslookup

set querytype=soa
```



### DNSSEC Zone Walking

Perform DNS enumeration using dnsrecon and find the IP address of the name server (ns2) for certifiedhacker.com.

162.159.25.175

```
dnsrecon.py -h
```

```
./dnsrecon.py -d <Target Domain> -z
```



### Nmap

Use nmap to perform DNS enumeration on certifiedhacker.com to gather the list of all the available DNS services on the target host along with their associated ports. What is the rDNS record for 162.241.216.11?

box5331.bluehost.com

```
nmap --script=broadcast-dns-service-discovery <Target Domain>
```

```
nmap -T4 -p 53 --script dns-brute <Target Domain>
```

```
nmap --script dns-srv-enum --script=args "dns-srv-enum.domain='<Target Domain>'"
```



## SMTP Enumeration

### Nmap

Use the Nmap to perform SMTP enumeration to enumerate the list of all the possible mail users on the Windows Server 2019 machine. Enter the number of users enumerated on the target machine.

10

```
nmap -p 25 --script=smtp-enum-users <Target IP address>
```



## RPC, SMP, FTP Enumeration

### NetScanTools Pro

Perform SMB enumeration using NetScanTools Pro. Is SMB version 1 (SMB 1) enabled on the machine at 10.10.1.19? (Yes/No)

No

### Nmap

Enumerate the machine at 10.10.1.19 using Nmap and find its http-server-header.

Microsoft-IIS/10.0

```
nmap -p 21 <Target IP address>
```

```
nmap -T4 -p <Target Port> -A <Target IP address>
```



## Enumeration using various Tools

### Global Network Inventory

Perform enumeration using Global Network Inventory and find the full name of the OS installed in the machine at 10.10.1.22.

Microsoft Windows Server 2022 Standard

### Advanced IP Scanner

Enumerate network resources using Advanced IP Scanner and find the version of the Apache httpd service running on the machine at 10.10.1.9.

2.4.52

### Enum4Linux

Enumerate users on the machine at 10.10.1.22 using Enum4linux and find the relative identifier (RID) for the user “shiela.”

0x451

```
enum4linux -u martin -p apple -U <Target IP address>
```

Enumerate the machine at 10.10.1.22 using Enum4linux and find its Platform\_ID.

500

```
enum4liux -u martin -p apple -o <Target IP address>
```

Enumerate the machine at 10.10.1.22 using Enum4linux and find its server type.

0x84102f

```
enum4liux -u martin -p apple -o <Target IP address>
```

