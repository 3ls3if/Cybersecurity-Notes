---
icon: browser
---

# Directory Enumeration

## Introduction

Directory Enumeration is a technique to find or identifying and listing the files and directories. directories enumeration can get the information about hidden file structure or sub directories.

Directory Enumeration can be performed by using dirb, dirbuster, gobuster and dirsearch.

## [Gobuster](https://github.com/OJ/gobuster)

```
gobuster dir -u http://172.17.0.1 -x php -w /usr/share/wordlists/dirb/common.txt
```

## Dirb

```
dirb http://172.17.0.1 /usr/share/wordlists/dirb/common.txt
```

## Wfuzz

```
wfuzz -c -z file,/usr/share/wordlists/dirb/common.txt --hc=404 http://127.0.0.1/FUZZ
```







***

## REFERENCES

* [https://medium.com/@infosecnubes/directory-enumeration-1ba91012dcf8](https://medium.com/@infosecnubes/directory-enumeration-1ba91012dcf8)
* [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)



