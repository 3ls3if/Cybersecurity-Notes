# Tasks

## Perform Session Hijacking

### Hijack Session using Zed Attack Proxy (ZAP)

Use the Zed Attack Proxy (ZAP) tool on the attacker machine (10.10.1.19) to hijack a session established when a user on the victim machine (10.10.1.11) visits the website www.goodshopping.com using the Chrome browser. Which ZAP tab allows you to edit web requests and responses?

Break



### Intercept HTTP Traffic using bettercap

In the Parrot Security machine, simulate the attacker and configure the bettercap tool to sniff the website www.moviescope.com accessed by the victim on the target system (10.10.1.11). Which bettercap module is responsible for sniffing the network?

net.sniff



### Intercept HTTP Traffic using Hetty

Use the Hetty tool to intercept HTTP traffic on the Windows Server 2022 machine. Enter the url that was entered in the address bar of the browser to open Hetty dashboard.

{% embed url="http://localhost:8080" %}

Use the Hetty tool to intercept HTTP traffic on the Windows Server 2022 machine. What was the password that was captured in Hetty tool by intercepting traffic of Windows Server 2022?

test



## Detect Session Hijacking

### Wireshark

Use the bettercap tool (available in the Parrot Security machine) to sniff the traffic on the target system (10.10.1.11). Use the Wireshark tool on the target system (10.10.1.11) to detect the session hijacking attempt. Traffic on which protocol indicates the session hijacking attempt in Wireshark?

ARP



