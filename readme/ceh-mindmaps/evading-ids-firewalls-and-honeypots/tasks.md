# Tasks

## Perform Intrusion Detection using Various Tools

### Detect Intrusions using Snort

Install Snort in the Windows Server 2019 machine. The necessary files are available at Z:\CEHv12 Module 12 Evading IDS, Firewalls, and Honeypots\Intrusion Detection Tools\Snort. Configure and initialize the Snort tool. Initialize the Snort interfaces and attack a target machine from the attacker machine (10.10.1.11) to check whether Snort detects it or not. Enter the Snort command to view the index number of the Ethernet driver.

```
snort -W
```



### Detect Malicious Network Traffic using ZoneAlarm FREE FIREWALL

Install the ZoneAlarm FREE FIREWALL tool in the Windows 11 machine located at E:\CEH-Tools\CEHv12 Module 12 Evading IDS, Firewalls, and Honeypots\Firewalls\ZoneAlarm FREE FIREWALL. Which zone will you use to block the website www.moviescope.com using the ZoneAlarm tool?

Blocked



### Detect Malicious Network Traffic using HoneyBOT

Install and configure the HoneyBOT tool on the Windows Server 2022 machine. The necessary files are available at Z:\CEHv12 Module 12 Evading IDS, Firewalls, and Honeypots\Honeypot Tools\HoneyBOT. View the complete details of the request or attack recorded by HoneyBOT from the attacker machine (10.10.1.13). Flag submission is not required for this task, enter "No flag" as the answer.

No flag



## Evade Firewalls using Various Evasion Techniques

### Bypass Firewall usinng Nmap&#x20;

Create an inbound firewall rule on the Windows 11 machine to block any incoming traffic through the Parrot Security machine. Perform a Zombie scan using the Nmap tool to view open ports and services on the Windows 11 machine. Enter the TCP port number used by the netbios-ssn service on Windows 11.

139

```
nmap -sI <Zombie machine IP> <Victim IP>
```



### Bypass Firewall Rules using HTTP/FTP Tunneling

Use HTTHost on the Windows Server 2022 machine and HTTPort on the Windows Server 2019 machine to bypass firewall restrictions. Which HTTPort tab will allow configuring a tunnel between the two machines?

Port mapping



### Bypass Antivirus using Metasploit

Modify Metasploit templates to bypass antivirus detection. Enter the new payload size that was entered in template.c file in this task.

4000

```
pluma /usr/share/metasploit-framework/data/templates/src/pe/exe/template.c
```

