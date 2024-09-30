# 🐕🦺 Service Enumeration

## FTP Enumeration

```
nmap -sC -p 21 <IP Address>
```

### Connect To The FTP Service

```
ftp <IP Address>
```

### Brute-Force FTP Service

```
hydra -L <username.txt> -P <password.txt> <IP Address> ftp
```

