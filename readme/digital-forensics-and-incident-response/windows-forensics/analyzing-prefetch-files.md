---
icon: file-chart-column
---

# Analyzing Prefetch Files

## Introduction

Prefetching is a Windows memory management process in which the operating system pre-loads resources from disk into memory as a means of speeding up the loading time for applications. As part of its process, a .pf file is created in the C:\Windows\Prefetch directory and updated each subsequent time the application is executed. The .pf file contains a list of resources, including files and directories that the executable referenced during execution, which is used to pre-load those resources the next time the application is executed.



## How Investigators Use Prefetch File Contents

The prefetch file, while not intended for analysis, can provide a wealth of information for an investigator. When opened, a prefetch file can show:

* Creation date – timestamped with the local time of the machine
* Date/time of last execution time – timestamped with the local time of the machine
* Run count – the number of times the executable has been launched
* Other run times – limited to the previous eight (8) executions
* Directories and files referenced – includes other executables
* Volumes and file paths – the location from which files were accessed

## Prefetch Analysis Tools

There are several tools available for reviewing the contents of prefetch files, including Eric Zimmerman’s PECmd command line tool and NirSoft’s WinPrefetchView.

PECmd is used for opening and reviewing the contents of .pf files. It supports several functions, including processing a single file or a directory of prefetch files. It can also output the .pf file information in a number of formats, including JSON, CSV, and HTML, as well as standard out. Zimmerman’s tool can be downloaded from GitHub at [https://github.com/EricZimmerman/PECmd](https://github.com/EricZimmerman/PECmd).

### [PECmd](https://github.com/EricZimmerman/PECmd)

```
PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf"
PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf" --json "D:\jsonOutput" --jsonpretty
PECmd.exe -d "C:\Temp" -k "system32, fonts"
PECmd.exe -d "C:\Temp" --csv "c:\temp" --csvf foo.csv --json c:\temp\json
PECmd.exe -d "C:\Windows\Prefetch"
```



Like PECmd, WinPrefetchView can open and review the individual contents of a .pf or pull in an entire prefetch directory.

\


<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

WinPrefetchView allows for the quick location and review of specific .pf files. However, it is limited in its report export functions allowing only HTML output. WinPrefetchView can be downloaded at [https://www.nirsoft.net/utils/win\_prefetch\_view.html](https://www.nirsoft.net/utils/win\_prefetch\_view.html).





***

## REFERENCES

* [https://trustedsec.com/blog/prefetch-the-little-snitch-that-tells-on-you](https://trustedsec.com/blog/prefetch-the-little-snitch-that-tells-on-you)
* [https://isc.sans.edu/diary/rss/29168  ](https://isc.sans.edu/diary/rss/29168https:/www.forensicfocus.com/articles/hunting-for-attackers-tactics-and-techniques-with-prefetch-files/https://or10nlabs.tech/prefetch-forensics/)
* [https://www.forensicfocus.com/articles/hunting-for-attackers-tactics-and-techniques-with-prefetch-files/  \
  https://or10nlabs.tech/prefetch-forensics/](https://isc.sans.edu/diary/rss/29168https:/www.forensicfocus.com/articles/hunting-for-attackers-tactics-and-techniques-with-prefetch-files/https://or10nlabs.tech/prefetch-forensics/)

