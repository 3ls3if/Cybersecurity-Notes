# 3306 - Mysql

## Theory

The MySQL database server uses TCP port 3306

* Brute‐forcing credentials&#x20;
* Identifying if the installed version is exploitable

***

## Practical

### Basic Nmap Scan

```
nmap ‐sV ‐O ‐sC ‐p 3306 [IP Address]
```

### Advanced Nmap Scan

```
nmap ‐sV ‐O ‐p 3306 ‐‐script=mysql* [IP Address]
```

### Brute Force

```
hydra ‐L [users file] ‐P [passwords file] MySQL://[IP]
```



***

## REFERENCES

* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql](https://book.hacktricks.xyz/network-services-pentesting/pentesting-mysql)
* [https://nmap.org/nsedoc/scripts/mysql-enum.html](https://nmap.org/nsedoc/scripts/mysql-enum.html)
