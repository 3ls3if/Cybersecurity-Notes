# 🔍 Network Scanning

## Nmap Commands

### Ping Sweep - Find Live Hosts

```
nmap -sP <IP Address>
```

### ARP Scan - Without Port Scan

```
nmap -PR -sn <IP Address>
```

### Scripts + Version Scan

```
nmap -sC -sV <IP Address>
```

### OS Scan

```
nmap -O <IP Address>
```

### Find Open Ports

```
nmap -p- <IP Address>
```

### Specific Port Scan

```
nmap -p <port number> <IP Address>
```

### Aggressive Scan

```
nmap -A <IP Address>
```

### NSE Scripts

```
nmap --script <script-name> -p <port number> <IP Address>
```

### Script + Version + Ports + OS Scan (Overall)

```
nmap -sC -sV -p- -A -v -T4 <IP Address>
```

