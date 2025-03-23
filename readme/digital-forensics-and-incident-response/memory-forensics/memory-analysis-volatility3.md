---
icon: memory
---

# Memory Analysis - Volatility3

## Memory Analysis using Volatility3

### Theory

Volatility is an open-source memory forensics framework for incident response and malware analysis. It is written in Python and supports Microsoft Windows, Mac OS X, and Linux. Volatility was created by Aaron Walters, drawing on academic research he did in memory forensics.



***

### Volatility3 Commands

### OS Information

1. OS Information

```
vol.py -f “/path/to/file” windows.info
```

### Process Information

#### pslist

```
vol.py -f “/path/to/file” windows.pslist

vol.py -f “/path/to/file” windows.psscan

vol.py -f “/path/to/file” windows.pstree
```

#### cmdline

```
vol.py -f “/path/to/file” windows.cmdline
```

#### DLLs

```
vol.py -f “/path/to/file” windows.dlllist ‑‑pid <PID>
```

### Network Information

#### netscan

```
vol.py -f “/path/to/file” windows.netscan

vol.py -f “/path/to/file” windows.netstat
```

### Registry

#### hivelist

```
vol.py -f “/path/to/file” windows.registry.hivescan

vol.py -f “/path/to/file” windows.registry.hivelist
```

### Files

#### Filescan

```
vol.py -f “/path/to/file” windows.filescan
```

#### Filedump

```
vol.py -f “/path/to/file” -o “/path/to/dir” windows.dumpfiles

vol.py -f “/path/to/file” -o “/path/to/dir” windows.dumpfiles ‑‑virtaddr <offset>

vol.py -f “/path/to/file” -o “/path/to/dir” windows.dumpfiles ‑‑physaddr <offset>
```



### Miscellaneous

#### Yarascan

```
vol.py -f “/path/to/file” windows.vadyarascan ‑‑yara-rules <string>

vol.py -f “/path/to/file” windows.vadyarascan ‑‑yara-file “/path/to/file.yar”

vol.py -f “/path/to/file” yarascan.yarascan ‑‑yara-file “/path/to/file.yar”
```

***

## REFERENCES

* [https://blog.onfvp.com/post/volatility-cheatsheet/](https://blog.onfvp.com/post/volatility-cheatsheet/)
* [https://volatilityfoundation.org/](https://volatilityfoundation.org/)
* [https://github.com/volatilityfoundation/volatility3](https://github.com/volatilityfoundation/volatility3)
