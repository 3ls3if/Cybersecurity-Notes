# IIS

## IIS Recon

### Find IIS server information

```
whatweb <IP addr>
```

### Access target server

```
http <IP addr>
```

### Find interesting files and directory

```
dirb http://<IP addr> 
```

### Access target webserver using CLI tool browsh

```
browsh --startup-url http://<IP addr>/Default.aspx
```



***

## Nmap Scripts

### Get sensitive information

```
nmap --script http-enum -sV -p 80 <IP addr>
```

### Run nmap http-headers script

```
namp --script http-headers -sV -p 80 <IP addr>
```

### Run nmap http-methods script to check all allowed methods

```
nmap --script http-methods --script-args http-methods.url-path=/webdav/ <IP addr> 
```

### Run webdav scanning namp script on /webdav directory

```
nmap --script http-webdav-scan --script-args http-methods.url-path=/webdav/ <IP addr>
```

