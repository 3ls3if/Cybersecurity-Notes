# 🐹 Stealth Scanning Strategies

When employing stealth to support reconnaissance, a tester mimicking the actions of a hacker will do the following:

* Camouflage tool signatures to avoid detection and triggering an alarm
* Hide the attack within legitimate traffic
* Modify the attack to hide the source and type of traffic
* Make the attack invisible using nonstandard traffic types or encryption

Stealth scanning techniques can include some or all of the following:

* Adjusting source IP stack and tool identification settings
* Modifying packet parameters (nmap)
* Using proxies with anonymity networks (ProxyChains and Tor network)



***

## Adjust Source IP Stack and Tool Identification Settings

### Disable IPv6

```
nano /etc/sysctl.conf

# Include the Follwoing Line
# disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable = 1
```

### Change User Agent

#### Metasploit

```
use auxiliary/fuzzers/http/http_form_field
set UserAgent Googlebot/2.1 (+http://www.google.com/bot.html)
```

* Legitimate User Agents: [`https://www.useragentstring.com`](https://www.useragentstring.com)



***

## Modify Packet Parameter

### Nmap Stealth Scan

```
nmap --spoof-mac-Cisco --data-length 24 –T paranoid --max-hostgroup
1  --max-parallelism 10 -PN -f –D 10.1.20.5,RND:5,ME --v –n –sS
–sV –oA /desktop/pentest/nmap/out –p T:1-1024 --random-hosts 10.1.1.10 10.1.1.15
```



***

## Using Proxy with Anonymity Networks (Tor and Privoxy)

### Proxychains4

```
#Install Tor
sudo apt install tor

#Edit Proxychains4.conf file
nano /etc/Proxychains.conf

#Comment the strict_chains options and uncomment the dynamic_chains options

#Add the below line in [ProxyList] section
socks5 127.0.0.1 9050

#Start Tor service
service tor start

#Verify 
service tor status

#Check your ip address
proxychains4 firefox www.whatismyip.com
```

{% hint style="info" %}
The Tor-Buddy script allows you to control how frequently the Tor IP address is refreshed, automatically making it more difficult to identify the user's information (http://sourceforge.net/projects/linuxscripts/ files/Tor-Buddy/).
{% endhint %}



***

