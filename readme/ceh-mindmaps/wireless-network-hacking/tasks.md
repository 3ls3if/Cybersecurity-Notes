# Tasks

## Footprint a Wireless Network

### Find Wi-Fi Networks Range using NetSurveyor

#### Tools

NetSurveyor



## Perform Wireless Traffic Analysis

### Find Wi-Fi Networks and Sniff Wi-Fi Packets using Wash and Wireshark

Use the Wi-Fi packet-sniffing tool Wireshark to analyze captured Wi-Fi packets (WEPcrack-01.cap). Enter the protocol that indicates the wireless packets. Note: sample captured Wi-Fi packets are available at E:\CEH-Tools\CEHv12 Module 16 Hacking Wireless Networks\Sample Captures.

802.11



## Perform Wireless Attacks

### Crack a WEP network using Aircrack-ng

Use the Aircrack-ng suite to crack the WEP encryption of a Wi-Fi network. Enter the key found in this exercise. Note: sample captured Wi-Fi packets are available at /home/attacker/Desktop/CEHv12 Module 16 Hacking Wireless Networks/Sample Captures.

98:48:35:97:49

```
aircrack-ng <pcap file>
```



### Crack a WPA2 Network using Aircrack-ng

Use the Aircrack-ng suite to crack a WPA2 network. Enter the key found in this exercise. Note: sample captured Wi-Fi packets and wordlist are available at /home/attacker/Desktop/CEHv12 Module 16 Hacking Wireless Networks

password1

```
aircrack-ng -a2 <Access Point MAC Address> -w /home/attacker/Desktop/passwor.txt /root/CEH-LABS-01.cap
```



