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

## REFERENCES

* [https://github.com/humblelad/Shodan-Dorks](https://github.com/humblelad/Shodan-Dorks)
