# ⛓️ DNS Recon and Route Mapping

## DNS Recon

The Domain Name System (DNS), is a distributed database that resolves names (www.digitaldefence.ca) to its IP addresses (192.150.2.140).

### Whois

```
whois <website>
```

{% hint style="info" %}
The returned whois record contains geographical information, names, and contact information—all of which can be used to facilitate a social engineering attack.
{% endhint %}

### Dnsrecon

```
dnsrecon -t std -d google.com
```

{% hint style="info" %}
DNSrecon allows the penetration tester to obtain the SOA record, name servers (NS), mail exchanger (MX) hosts, servers sending e-mails using Sender Policy Framework (SPF), and the IP address ranges in use.
{% endhint %}

### dnsdict6

```
dnsdict6 google.com
```



***

## Mapping the Route to the Target

Route mapping was originally used as a diagnostic tool that allows you to view the route that an IP packet follows from one host to the next. Using the time to live (TTL) field in an IP packet, each hop from one point to the next elicits an ICMP TIME\_EXCEEDED message from the receiving router, decrementing the value in the TTL field by 1. The packets count the number of hops and the route taken.

### Traceroute

#### Linux

```
traceroute www.google.com
```

#### Windows

```
tracert <IP>
```

### Hping3

```
hping3 -S www.google.com -p 80 -c 3
```

* \-S : TCP with SYN flag set
* \-p : Direct the packet to port 80
* \-c : Set the count of sending three packets to the target

{% hint style="info" %}
The hping3 command successfully identifies that the target is online, and provides some basic routing information.
{% endhint %}

