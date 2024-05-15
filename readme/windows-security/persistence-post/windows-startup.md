# Windows Startup

## Windows Startup

### Theory

When attackers compromise hosts and plant malware, one of the key objectives is gain persistence. Writing a malware on a host does not warrant it survives reboot. In order to persist, the Startup directory can be used. Achieving persistence on systems running Windows utilizing the Startup directory is no news. The technique is also documented in the MITRE ATT\&CK framework as T1060.

### Practical

#### Startup Folder

```
Current User
Windows XP
C:\Documents and Settings\%USERNAME%\Start Menu\Programs\Startup
Windows Vista and later
C:\Users\%USERNAME%\Start Menu\Programs\Startup

All Users
Windows XP
C:\Documents and Settings\All Users\Start Menu\Programs\Startup
Windows Vista and later
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup

```

#### Registry

```
Current User
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce

All Users
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce

```

```
Current User
REG ADD HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run /v calc /t REG_SZ /d C:\Windows\System32\calc.exe

All users
REG ADD HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run /v calc /t REG_SZ /d C:\Windows\System32\calc.exe
```

***

## References

* https://azeria-labs.com/persistence/
* https://www.cyborgsecurity.com/cyborg-labs/hunting-for-persistence-registry-run-keys-startup-folder/
* https://stmxcsr.com/persistence/looking-at-the-startup-directory.html
