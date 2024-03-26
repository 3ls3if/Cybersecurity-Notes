# 1521 - Oracle DB Server

## Theory

The Oracle database server uses TCP port 1521, and the same concepts apply to it as Microsoft SQL Server when it comes to enumeration:

* Brute‐forcing credentials
* Identifying if the installed version is exploitable

***

## Practical

### Basic Nmap Scan

```
nmap ‐sV ‐O ‐sC ‐p 1521 [IP Address]
```

### Advanced Nmap Scan

```
nmap ‐sV ‐O ‐p 1521 ‐‐script=oracle* [IP Address]
```

### Brute Force

#### Hydra

```
hydra ‐s 1521 ‐L [users file] ‐P [passwords file] [IP]
```



***

## REFERENCES

* [https://book.hacktricks.xyz/network-services-pentesting/1521-1522-1529-pentesting-oracle-listener](https://book.hacktricks.xyz/network-services-pentesting/1521-1522-1529-pentesting-oracle-listener)
* [https://secybr.com/posts/oracle-pentesting-best-practices/](https://secybr.com/posts/oracle-pentesting-best-practices/)
