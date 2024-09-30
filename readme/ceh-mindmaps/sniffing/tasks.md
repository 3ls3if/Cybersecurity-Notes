# Tasks

## Perform Active Sniffing

### MAC Flooding using macof

Use macof on the Parrot Security machine to perform MAC flooding on the Windows 11 target machine. What is the default size of the IP packets that macof uses to flood the CAM table with random MAC addresses?

54

```
macof -i eth0 -n 10
```



### DHCP Starvation Attack using Yersinia

Use Yersinia on the Parrot Security machine to perform a DHCP starvation attack. What is the default source port used by Yersinia in the DHCP mode?

00068



### ARP Poisoning using arpspoof

Use arpspoof on the Parrot Security machine to perform an ARP poisoning attack. What is the default size/length of the ARP packets that arpspoof uses to poison the CAM table?

42

```
arpspoof -i eth0 10.10.1.11 10.10.1.1
```



### MITM attack using Cain & Abel

Run Cain and Abel on the Windows Server 2019 machine and perform an MITM attack to sniff traffic between the Windows Server 2022 and Windows 11 machines. Which tab under Cain lists all the discoverable machines in the network?

Sniffer



### Spoof MAC address using TMAC and HMAC

On the Windows 11 machine, use the SMAC tool to spoof the MAC address of the machine. Flag submission is not required for this task, enter "No flag" as the answer.

No flag



### Macchanger

Using macchanger utility to change the MAC address of the Parrot Security machine. Enter the option that prints the MAC address of the machine.

\-s

```
macchanger -s eth0
```

Using macchanger utility to change the MAC address of the Parrot Security machine. Enter the option that sets random vendor MAC address to the network interface.

\-a

```
macchanger -a eth0
```



## Network Sniffing using Various Tools

### Password Sniffing using Wireshark

Use the Wireshark tool to perform password sniffing. Which Wireshark display filter shows HTTP POST traffic?

```
http.request.method == POST
```



### Analyze a Network&#x20;

#### Omnipeek Network Protocol Analyzer

Use the Omnipeek Network Protocol Analyzer on the Windows 11 machine to analyze the network. (This is an optional task. You need to register on https://www.liveaction.com/products/omnipeek-network-protocol-analyzer/ and create a 30-Day Trial account to perform this task. Flag submission is not required for this task, enter "No flag" as the answer.

No flag



#### SteelCentral Packet Analyzer

Use the SteelCentral Packet Analyzer on the Windows 11 machine to analyze the network. (This is an optional task. You need to register on https://www.riverbed.com/in/trialdownloads.html and create a Trial account to perform this task. Flag submission is not required for this task, enter "No flag" as the answer.

No flag



## Detect Network Sniffing

### Detect ARP Poisoning and Promiscuous Mode

Use Cain and Abel on the Windows Server 2019 machine to perform ARP poisoning, and sniff traffic between the Windows 11 and Parrot Security machines. Further, use Wireshark on the same Windows Server 2019 machine to detect ARP poisoning. What is the severity level of ARP/RARP packets as shown in the expert information window of Wireshark?

Warning



```
Open Wireshark

Click on Analyze

Expert Information
```



Use the Nmap Scripting Engine (NSE) to check if a system on the local Ethernet has its network card in the promiscuous mode. Which Nmap NSE script detects if a network interface is in the promiscuous mode?

sniffer-detect

```
nmap --script=sniffer-detect <IP address>
```



### Detect ARP Poisoning using the Capsa Network Analyzer

Use Habu tool to perform ARP poisoning attack on the target system and use Capsa Network Analyser to detect the attack. Enter the IP address of the attacker machine that was located in the Node Explorer.

10.10.1.13

#### Start ARP Poisoning

```
habu.arp.poison 10.10.1.11 10.10.1.13
```

