---
icon: vr-cardboard
---

# Identify Virtual Websites

## Introduction

Virtual hosting is a feature that allows a single web server to host multiple websites and have them appear as if they are hosted on separate, individual servers. This is usually done to reduce resource overhead and running costs.

There are two types of virtual hosting: IP-based and Name-based.

## FFUF

```
ffuf -w namelist.txt -u http://10.129.184.109 -H "HOST: FUZZ.inlanefreight.htb".

# Filtering Response Size
fuf -w namelist.txt -u http://10.129.184.109 -H "HOST: FUZZ.inlanefreight.htb" -fs 10918
```

## /etc/hosts File

```
# Add the IP and Domain mapping in the /etc/hosts file

10.10.10.10    example.com
```

## Dig Utility

```
dig AXFR @10.10.10.10 example.com +nostat +nocmd +nocomments
```







***

## REFERENCES

* [https://www.freecodecamp.org/news/virtual-host-enumeration-tutorial/](https://www.freecodecamp.org/news/virtual-host-enumeration-tutorial/)



