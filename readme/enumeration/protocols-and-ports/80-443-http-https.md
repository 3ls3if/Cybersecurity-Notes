# 80, 443 - HTTP, HTTPS

## Theory

### HTTP TCP Port 80

This serves cleartext web requests and responses. If you sniff the network of a website that serves on port 80, you will be able to see the login credentials in cleartext.

### HTTPS/TLS TCP Port 443

The secure protocol of the HTTP protocol is called HTTPS or TLS. The communication is secure, so a sniffer won't be able to view the traffic unless there is a proxy that intercepts the traffic. Big companies use proxies and inject certificates into the user's host so they'll be able to monitor the HTTPS traffic of their employees.

{% hint style="info" %}
Web portals like Jenkins, for example, don't use the default port number 80 to avoid conflicting with the default web application hosted on the same web server.
{% endhint %}



***

## Practical

### Basic Nmap Scan

```
nmap -sV --script=http-enum <target>

nmap -sV --script=http-userdir-enum <target>
```

### Basic Whatweb Scan

```
whatweb -a 1 <URL> #Stealthy
whatweb -a 3 <URL> #Aggresive
webtech -u <URL>
webanalyze -host https://google.com -crawl 2
```

### Automatic Scanners

```
nikto -h <URL>
whatweb -a 4 <URL>
wapiti -u <URL>
W3af
zaproxy #You can use an API
nuclei -ut && nuclei -target <URL>

# https://github.com/ignis-sec/puff (client side vulns fuzzer)
node puff.js -w ./wordlist-examples/xss.txt -u "http://www.xssgame.com/f/m4KKGHi2rVUN/?query=FUZZ"
```

### CMS Scanners

```
cmsmap [-f W] -F -d <URL>
wpscan --force update -e --url <URL>
joomscan --ec -u <URL>
joomlavs.rb #https://github.com/rastating/joomlavs
```



***

## REFERENCES

* [https://book.hacktricks.xyz/network-services-pentesting/pentesting-web](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web)

