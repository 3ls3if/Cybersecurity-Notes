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

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>Pcredz Example</p></figcaption></figure>

#### Ngrep

Install ngrep

```
sudo apt install ngrep
```

If you are **looking** for **something** inside the pcap you can use **ngrep**. Here is an example using the main filters:

```
ngrep -I packets.pcap "^GET" "port 80 and tcp and host 192.168 and dst host 192.168 and src host 192.168"
```

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Ngrep Example</p></figcaption></figure>



***

## REFERENCES

* [https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection](https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection)
* [https://github.com/lgandx/PCredz](https://github.com/lgandx/PCredz)
* [https://github.com/ShellCode33/CredSLayer](https://github.com/ShellCode33/CredSLayer)
* [https://github.com/DanMcInerney/net-creds](https://github.com/DanMcInerney/net-creds)



