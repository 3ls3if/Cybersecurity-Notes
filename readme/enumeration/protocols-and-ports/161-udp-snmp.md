# 161 UDP - SNMP

## Theory

The Simple Network Management Protocol is a database that stores network devices/hosts information (for network management purposes). The SNMP information database is called Management Information Base (MIB), and it structures data in a tree. This server uses UDP port 161 to expose this information. The prior versions of SNMP 1, 2, and 2c don't use encryption in the traffic, so using a sniffer will allow us to intercept the cleartext credentials. The SNMP server uses a community string to secure the data inside the server.

You can use the following three community strings to connect to the SNMP server:

* Public
* Private
* Manager

### SNMP Enumeration

If you were able to enumerate the SNMP server, then you will see a lot of important information about the target host:

* Network interfaces&#x20;
* Listening ports&#x20;
* System processes&#x20;
* Host hardware information&#x20;
* Software installed&#x20;
* Local users&#x20;
* Shared folders



***

## Practical

### Nmap Scan

```
nmap -sU -p 161 -sV -sC -T5 <IP>
```

### [Snmp-Check](https://www.kali.org/tools/snmpcheck/)

```
snmp-check 192.168.1.2 -c public
```

### Snmp-Bulk-Walk

```
snmpbulkwalk -c [COMM_STRING] -v [VERSION] [IP] . #Don't forget the final dot
snmpbulkwalk -c public -v2c 10.10.11.136 .
```

### Snmp-Walk

```
snmpwalk -v [VERSION_SNMP] -c [COMM_STRING] [DIR_IP]
```

***

## REFERENCES

* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp](https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp)
* [https://www.kali.org/tools/snmpcheck/](https://www.kali.org/tools/snmpcheck/)

