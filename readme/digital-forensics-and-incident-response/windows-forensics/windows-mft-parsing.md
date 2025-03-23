---
icon: table
---

# Windows MFT Parsing

## Introduction

In computer forensics, the Master File Table (MFT) is a crucial component of the Windows operating system. It is a database that contains essential information about every file and directory on a computer's hard drive. The MFT keeps track of a file's location on the hard drive and manages other attributes. It contains metadata about each file, such as its name, size, creation date, and access permissions. They understand this data is critical for any computer forensics examination.

## Tools to Extract MFT

[Jeff Bryner - MFT Grabber](https://github.com/jeffbryner/pyMFTGrabber)

[NTFS Walk](https://tzworks.com/prototype\_page.php?proto\_id=12)

[Eric Zimmerman - MFTECmd](https://github.com/EricZimmerman/MFTECmd)

## [MFTECmd](https://github.com/EricZimmerman/MFTECmd)

```
MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out" --csvf MyOutputFile.csv
MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out"
MFTECmd.exe -f "C:\Temp\SomeMFT" --json "c:\temp\jsonout"
MFTECmd.exe -f "C:\Temp\SomeMFT" --body "c:\temp\bout" --bdl c
MFTECmd.exe -f "C:\Temp\SomeMFT" --de 5-5
```







***

## REFERENCES

* [https://www.asdfed.com/Master-File-Table-and-Computer-Forensics](https://www.asdfed.com/Master-File-Table-and-Computer-Forensics)
* [https://aboutdfir.com/toolsandartifacts/windows/mft-explorer-mftecmd/](https://aboutdfir.com/toolsandartifacts/windows/mft-explorer-mftecmd/)
* [https://binaryforay.blogspot.com/2018/06/introducing-mftecmd.html](https://binaryforay.blogspot.com/2018/06/introducing-mftecmd.html)
* [https://github.com/EricZimmerman/MFTECmd](https://github.com/EricZimmerman/MFTECmd)
