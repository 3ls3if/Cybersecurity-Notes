# 🔄 Router

{% embed url="https://null-byte.wonderhowto.com/how-to/configure-port-forwarding-create-internet-connected-services-0182008/" %}

### Identify The IP Address of Gateway

#### Windows

```
ipconfig /all
```

#### Linux

```
netstat -rn
```



### Access the Router Configuration Panel

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

While all routers will have slightly different interfaces, once logged in, look for an "Advanced" area, or something which includes "Port Forwarding." In the case below, the relevant area was titled "Advanced Port Forwarding Rules."

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Now, you can begin configuring port forwarding settings for the router.
{% endhint %}

###

### Define Your Port Forwarding Rules

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

### Protect from Port Scanning & Attacks

In the case of port forwarding, to protect against port scanning, it may be advantageous to change the public or source port in the router configuration. Rather than using a common port like 22, which is frequently scanned for, a more uncommon port such as 9022 can serve just as well to connect over SSH to the Raspberry Pi without leaving a low-numbered port available to be discovered through scanning.

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

With this port changed, the only difference in usage is that a client connecting to the devices over SSH from outside the network will need to specify port 9022 rather than assuming the default port, 22, is in use. Attempting to connect to port 22 will not work outside of the local network, as while the SSH daemon on the Pi is running on that port, it is being forwarded over port 9022, not port 22.

You can also use a service like [Fail2ban](https://www.fail2ban.org/wiki/index.php/Main\_Page), an intrusion prevention software framework designed to protect your system from brute-force attacks once an attacker finds out the real port you're using. A tool like Fail2ban will rate-limit the number of login attempts that can be made on the network.

