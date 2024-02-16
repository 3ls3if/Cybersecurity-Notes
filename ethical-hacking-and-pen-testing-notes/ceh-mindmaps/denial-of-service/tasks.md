# Tasks

## Perform DoS and DDoS&#x20;

### Perform DoS Attack (SYN Flooding) using Metasploit

Use Metasploit on the Parrot Security machine (10.10.1.13) to perform a SYN flooding attack against the Windows 11 machine (10.10.1.11) through port 21. Which auxiliary module will you use in msfconsole to launch the attack?

```
auxiliary/dos/tcp/synflood
```



### Perform DoS Attack on a Target Host using Hping3

Use the hping3 tool on the Parrot Security machine to launch DoS attacks such as SYN flooding, ping of death (PoD), and UDP application layer flood attacks on the target Windows 11 host. Which hping3 parameter will allow using a spoofed source address?

\-a

```
hping3 -S <Target IP address> -a <Spoofable IP address> -p 22 --flood
```



### Perform DoS Attack using Raven-storm

Use Raven-storm tool to perform a DoS attack on Windows Server 2019. Enter the command that is used to load layer 4 (UDP/TCP) module in Raven-storm tool.

```
l4
```

```
sudo rst

l4

ip 10.10.1.19

port 80

threads 20000

run

Y
```



Use Raven-storm tool to perform a DoS attack on Windows Server 2019. Enter the command that is used to load layer 7 (HTTP) module in Raven-storm tool.

```
l7
```



### Perform a DDoS Attack using HOIC

Use the HOIC tool on the Windows 11, Windows Server 2019, and Windows Server 2022 machines to launch a DDoS attack on the Parrot Security machine. Which button on HOIC is used to launch the attack?

FIRE TEH LAZER!



### Perform a DDoS Attack using LOIC

Use the LOIC tool on the Windows 11, Windows Server 2019, and Windows Server 2022 machines to launch a DDoS attack on the Parrot Security machine. What is the default timeout value for the LOIC attack?

9001



## Detect and Protect Against DoS and DDoS Attack

### Anti DDoS Guardian

For this task, first use the LOIC tool on the Windows Server 2019 and Windows Server 2022 machines to perform a DDoS attack on the Windows 11 target system. Then, use the Anti DDoS Guardian tool on the Windows 11 machine to detect and protect against the DDoS attack. Which Anti DDoS Guardian option will you use to stop an ongoing DoS attack?

Block IP

