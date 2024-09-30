# Pcap Analysis

## Extract Information from a Pcap File

### Extract Credentials

#### Pcredz

Install Pcredz

```
apt install python3-pip && sudo apt-get install libpcap-dev && pip3 install Cython && pip3 install python-libpcap

# extract credentials from a pcap file
python3 ./Pcredz -f file-to-parse.pcap

# extract credentials from all pcap files in a folder
python3 ./Pcredz -d /tmp/pcap-directory-to-parse/

# extract credentials from a live packet capture on a network interface (need root privileges)
python3 ./Pcredz -i eth0 -v
```

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Pcredz Example</p></figcaption></figure>

#### Ngrep

Install ngrep

```
sudo apt install ngrep
```

If you are **looking** for **something** inside the pcap you can use **ngrep**. Here is an example using the main filters:

```
ngrep -I packets.pcap "^GET" "port 80 and tcp and host 192.168 and dst host 192.168 and src host 192.168"
```

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Ngrep Example</p></figcaption></figure>



### Extract Information

#### Scapy

```
# Install Scapy
pip3 install scapy

# Start Scapy
scapy

# Read pcap file
pcap = rdpcap('tftp_rrq.pcap')

# Display graph of conversations
pcap.conversations()

# Display sessions
pcap.sessions()

# displays a list of summaries of each packet
pcap.summary()

# Display source ip address
for pkt in pcap:
     print(pkt[IP].src)


```

#### More Scapy Commands

| summary()       | displays a list of summaries of each packet                |
| --------------- | ---------------------------------------------------------- |
| nsummary()      | same as previous, with the packet number                   |
| conversations() | displays a graph of conversations                          |
| show()          | displays the preferred representation (usually nsummary()) |
| filter()        | returns a packet list filtered with a lambda function      |
| hexdump()       | returns a hexdump of all packets                           |
| hexraw()        | returns a hexdump of the Raw layer of all packets          |
| padding()       | returns a hexdump of packets with padding                  |
| nzpadding()     | returns a hexdump of packets with non-zero padding         |
| plot()          | plots a lambda function applied to the packet list         |
| make\_table()   | displays a table according to a lambda function            |





## REFERENCES

* [https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection](https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection)
* [https://github.com/lgandx/PCredz](https://github.com/lgandx/PCredz)
* [https://github.com/ShellCode33/CredSLayer](https://github.com/ShellCode33/CredSLayer)
* [https://github.com/DanMcInerney/net-creds](https://github.com/DanMcInerney/net-creds)
* [https://www.sans.org/blog/sans-pen-test-cheat-sheet-scapy/](https://www.sans.org/blog/sans-pen-test-cheat-sheet-scapy/)
* [https://scapy.readthedocs.io/en/latest/usage.html](https://scapy.readthedocs.io/en/latest/usage.html)



