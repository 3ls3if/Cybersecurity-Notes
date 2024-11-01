---
icon: web-awesome
---

# Shodan

## Shodan Dorks

_Dorks for shodan.io_ website. Taken from publicly available sources.

## Shodan

_Shodan is a search engine that lets the user find specific types of computers (webcams, routers, servers, etc.) connected to the internet using a variety of filters._

### Basic Shodan Filters

#### city:

Find devices in a particular city.\
`city:"Bangalore"`

#### country:

Find devices in a particular country.\
`country:"IN"`

#### geo:

Find devices by giving geographical coordinates.\
`geo:"56.913055,118.250862"`

#### hostname:

Find devices matching the hostname.\
`server: "gws" hostname:"google"`

#### net:

Find devices based on an IP address or /x CIDR.\
`net:210.214.0.0/16`

#### os:

Find devices based on operating system.\
`os:"windows 7"`

#### port:

Find devices based on open ports.\
`proftpd port:21`

#### before/after:

Find devices before or after between a given time.\
`apache after:22/02/2009 before:14/3/2010`

#### Citrix:

Find Citrix Gateway.\
`title:"citrix gateway"`

#### Wifi Passwords:

Helps to find the cleartext wifi passwords in Shodan.\
`html:"def_wirelesspassword"`

#### Surveillance Cams:

With username:admin and password: :P\
`NETSurveillance uc-httpd`

#### Fuel Pumps connected to internet:

No auth required to access CLI terminal.\
`"privileged command" GET`

#### Windows RDP Password:

But may contain secondary windows auth\
`"\x03\x00\x00\x0b\x06\xd0\x00\x00\x124\x00"`

#### Mongo DB servers:

It may give info about mongo db servers and dashboard\
`"MongoDB Server Information" port:27017 -authentication`

#### FTP servers allowing anonymous access:

Complete Anon access\
`"220" "230 Login successful." port:21`

#### Jenkins:

Jenkins Unrestricted Dashboard\
`x-jenkins 200`

#### Hacked routers:

Routers which got compromised\
`hacked-router-help-sos`

#### Open ATM:

May allow for ATM Access availability\
`NCR Port:"161"`

#### Telnet Access:

NO password required for telnet access.\
`port:23 console gateway`

#### Misconfigured Wordpress Sites:

The wp-config.php if accessed can give out the database credentials.\
`http.html:"* The wp-config.php creation script uses this file"`

#### Hiring:

Find sites hiring.\
`"X-Recruiting:"`

#### Android Root Bridge:

Find android root bridges with port 5555.\
`"Android Debug Bridge" "Device" port:5555`

#### Etherium Miners:

Shows the miners running ETH.\
`"ETH - Total speed"`

#### Tesla Powerpack charging Status:

Helps to find the charging status of tesla powerpack.\
`http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2`&#x20;

#### Unauthenticated Kibana Endpoints

```
kibana content-length:217
```



***

## Website Exercises

* **Find the 4SICS website using Shodan.**

```
title:4sics
```

* **Find the Rastalvskarn powerplant.**

{% hint style="info" %}
**Tip:** It is running anonymous VNC and is located in the Swedish city of Nora
{% endhint %}

```
has_screenshot:1 country:se city:nora
```

* **How many IPs in Sweden are vulnerable to Heartbleed and still support SSLv2?**
* **How many IPs are vulnerable to Heartbleed at your organization?**

```
vuln:CVE-2014-0160 country:se ssl.version:sslv2
vuln:CVE-2014-0160 org:"your organization"
```

* **Find all the industrial control systems in your town.**

```
category:ics city:"your city name"
```

* **Which RAT is most popular in Sweden?**

```
category:malware country:se
```

***

## Command Line Interface Exercises

* **Download the IPs vulnerable to Heartbleed in Sweden and Norway using the Shodan CLI. Filter out the results for Sweden and store them in a separate file.**

{% hint style="info" %}
**Note:** Uncompress the file and look at the raw data to see the raw response from the Heartbleed test.
{% endhint %}

```
shodan download --limit -1 heartbleed-results country:se,no vuln:CVE-2014-0160
shodan parse --filters location.country_code:SE -O heartbleed-sweden heartbleed-\
results.json.gz
```

{% hint style="info" %}
**Note:** The –filters argument does case-sensitive searching on properties that are strings, hence the Swedish country code has to be upper-case.
{% endhint %}

* **Download 1,000 recent banners using the real-time stream and then map them using Google Maps.**

{% hint style="info" %}
**Tip:** shodan convert
{% endhint %}

```
mkdir data
shodan stream --limit 1000 --datadir data/
shodan convert data/* kml
```

{% hint style="info" %}
## Upload the KML file to https://www.google.com/maps/d/
{% endhint %}

* **Write a script to download a list of known malware IPs and block any outgoing traffic to them.**

{% hint style="info" %}
Tip: iptables -A OUTPUT -d x.x.x.x -j DROP
{% endhint %}

```bash
#!/bin/bash
shodan download --limit -1 malware.json.gz category:malware
for ip in `shodan parse --fields ip_str malware.json.gz`
do
iptables -A OUTPUT -d $ip -j DROP
done
```



***

## Shodan API Exercises

* **Write a script to monitor a network using Shodan and send out notifications.**

```python
#!/usr/bin/env python
# Initialize Shodan
import shodan
api = shodan.Shodan("YOUR_API_KEY")
# Create a new alert
alert = api.create_alert('My first alert', '198.20.69.0/24')
try:
    # Subscribe to data for the created alert
    for banner in api.stream.alert(alert['id']):
    print banner
except:
    # Cleanup if any error occurs
    api.delete_alert(alert['id'])
```

{% hint style="info" %}
**Tip:** Use the Shodan command-line interface’s alert command to list and remove alerts. For example:
{% endhint %}

```
shodan alert list
shodan alert clear
```

* **Write a script to output the latest images into a directory**

{% hint style="info" %}
**Tip:** Images are encoded using base64. Python can easily decode it into binary using: image\_string.decode(‘base64’)
{% endhint %}

```
mkdir images
```

{% hint style="info" %}
Run the above command to generate a directory to store the images in. Then save the following code in a file such as image-stream.py:
{% endhint %}

```python
#!/usr/bin/env python
import shodan
output_folder = 'images/'
api = shodan.Shodan("YOUR_API_KEY")
for banner in api.stream.banners():
    if 'opts' in banner and 'screenshot' in banner['opts']:
    # All the images are JPGs for now
    # TODO: Use the mimetype to determine file extension
    # TODO: Support IPv6 results
    # Create the file name using its IP address
        filename = '{}/{}.jpg'.format(output_folder, banner['ip_str'])
        # Create the file itself
        output = open(filename, 'w')
        # The images are encoded using base64
        output.write(banner['opts']['screenshot'].decode('base64'))
```



***

## REFERENCES

* [https://github.com/humblelad/Shodan-Dorks](https://github.com/humblelad/Shodan-Dorks)
