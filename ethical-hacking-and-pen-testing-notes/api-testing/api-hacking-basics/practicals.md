# Practicals

### Communicating with APIs

Scanning with namp

```
nmap -sV 172.105.55.98
```

Fuzzing with ffuf

```
ffuf -w params.txt:PARAM -w values.txt:VAL -u https://example.org/?PARAM=VAL -mr "VAL" -c
```

