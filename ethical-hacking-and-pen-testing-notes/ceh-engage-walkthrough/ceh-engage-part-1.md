# 1⃣ 1⃣ CEH Engage Part 1

Perform vulnerability scanning for the webserver hosting movies.cehorg.com using OpenVAS and identify the severity level of RPC vulnerability.

```
nmap -sn moves.cehorg.com
```

<figure><img src="../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>



Perform vulnerability scanning for the Linux host in the 172.16.0.0/24 network using OpenVAS and find the number of vulnerabilities with severity level as medium.

<figure><img src="../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>



You are performing reconnaissance for CEHORG and has been assigned a task to find out the physical location of one of their webservers hosting www.certifiedhacker.com. What are the GEO Coordinates of the webserver? Note: Provide answer as Latitude, Longitude.

#### BillCipher

<figure><img src="../../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

Identify if the website www.certifiedhacker.com allows DNS zone transfer. (Yes/No)

```
dig www.certifiedhacker.com -axfr
```

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

Identify the number of live machines in 172.16.0.0/24 subnet.

```
nmap -sn -PE 172.16.0.0/24
```

<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>



While performing a security assessment against the CEHORG network, you came to know that one machine in the network is running OpenSSH and is vulnerable. Identify the version of the OpenSSH running on the machine. Note: Target network 192.168.0.0/24.

```
sudo nmap -sV -p 22 192.168.0.0/24
```

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

During a security assessment, it was found that a server was hosting a website that was susceptible to blind SQL injection attacks. Further investigation revealed that the underlying database management system of the site was MySQL. Determine the machine OS that hosted the database.



```
 sudo nmap -sV -O -A -p 3306 192.168.55
```

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

Find the IP address of the Domain Controller machine in 10.10.10.0/24.

```
nmap -sV -A -T4 10.10.10.0/24
```

<figure><img src="../../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>





Perform a host discovery scanning and identify the NetBIOS name of the host at 10.10.10.25.

```
nmap -sV -A -T4 10.10.10.25
```

<figure><img src="../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

Find the IP address of the machine which has port 21 open. Note: Target network 172.16.0.0/24

```
nmap -p 21 172.16.0.0/24
```

<figure><img src="../../.gitbook/assets/image (160).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>



Perform an intense scan on 10.10.10.25 and find out the FQDN of the machine in the network.

```
nmap -sV -A -T4 10.10.10.25
```

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>



What is the DNS Computer Name of the Domain Controller?

```
nmap -sV -A -T4 10.10.10.25
```

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>



Perform LDAP enumeration on the target network and find out how many user accounts are associated with the domain.

```
ldapsearch -x -h 10.10.10.25 -b "DC=CEHORG,DC=com" "objectclass=user" cn
```

<figure><img src="../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>









Perform an LDAP Search on the Domain Controller machine and find out the version of the LDAP protocol.

```
ldapsearch -h 10.10.10.25 -x -s base namingcontexts
```

<figure><img src="../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>



What is the IP address of the machine that has NFS service enabled? Note: Target network 192.168.0.0/24.

```
sudo nmap -sV -p 2049 192.168.0.0/24
```



<figure><img src="../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>









Perform a DNS enumeration on www.certifiedhacker.com and find out the name servers used by the domain.

```
dnsenum www.certifiedhacker.com
```

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>









Find the IP address of the machine running SMTP service on the 192.168.0.0/24 network.

```
nmap -sV -T4 -p 25 192.168.0.0/25
```

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>









![](https://www.cyberq.io/assets/img/svgIcons/flagRed.png)

Perform an SMB Enumeration on 192.168.0.51 and check whether the Message signing feature is enabled or disabled. Give your response as Yes/No.

```
nmap -A -T4 192.168.0.51
```

<figure><img src="../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>





Perform vulnerability scanning for the domain controller using OpenVAS and identify the number of vulnerabilities with severity level as "medium".

<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>





Perform a vulnerability research on CVE-2022-30171 and find out the base score and impact of the vulnerability.

{% embed url="https://nvd.nist.gov/vuln/" %}

<figure><img src="../../.gitbook/assets/image (161).png" alt=""><figcaption></figcaption></figure>
