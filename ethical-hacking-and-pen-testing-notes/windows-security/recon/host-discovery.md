# Host Discovery

## Powershell Network  Scanner

{% embed url="https://github.com/BornToBeRoot/PowerShell_IPv4NetworkScanner" %}

```
PS> .\IPv4NetworkScan.ps1 -IPv4Address 192.168.178.0 -Mask 255.255.255.0 -DisableDNSResolving
```

```
PS> .\IPv4NetworkScan.ps1 -IPv4Address 192.168.178.0 -CIDR 20
```



***

## Zenmap

{% embed url="https://nmap.org/zenmap/" %}



***

## Nmap

```
nmap -Pn <IP address>
```

```
nmap -Pn -p 80 <IP address>
```

```
nmap -Pn -p 80 -sV <IP address>
```

