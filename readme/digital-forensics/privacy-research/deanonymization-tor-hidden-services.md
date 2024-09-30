---
description: >-
  This article is taken from this DefCon talk::
  https://www.youtube.com/watch?v=v45_tkKCJ54
icon: user-ninja
---

# Deanonymization - TOR Hidden Services

## Common Approaches

* **Traffic Analysis**: Examining patterns in network traffic to infer relationships or identify users.
* **Timing Attacks**: Measuring the timing of data packets to potentially deanonymize users.
* **Correlation Attacks**: Matching incoming and outgoing traffic to reveal hidden service identities.
* **Endpoint Compromise**: Gaining access to the servers hosting hidden services to extract information.



## Hidden Service

Allow users to publish their service without revealing their identity&#x20;

**Configuration**&#x20;

```
HiddenServiceDir  /var/lib/tor/hidden_service/ 
HiddenServicePort 80 127.0.0.1:80 
```

**Hidden service address**&#x20;

```
mhphb7utr2eqmul5mgggk5apf6dyjlldgujfvxohjiqu5pd2b7scg6qd.onion
```



## Known Deanonymization Techniques

<figure><img src="../../../.gitbook/assets/image (214).png" alt=""><figcaption><p>known deanonymization techniques</p></figcaption></figure>

### 1. http://\*.onion/server-status

<figure><img src="../../../.gitbook/assets/image (215).png" alt=""><figcaption><p>server-status route</p></figcaption></figure>

### 2. Key Certificate

* TLS certificate might be indexed on the surface web and can lead to the same resource from the dark net or other services of the same actor
* Shodan indexes information from the internet including TLS information

<figure><img src="../../../.gitbook/assets/image (217).png" alt=""><figcaption><p>Key Certificate</p></figcaption></figure>

### 3. Search for onion address

* Very little chance of success
* Just search the onion address on search engines like Google, Bing, DuckDuckGo or Shodan



### 4. GZIP Compression

* Jose Carlos found that around 10% of the webservers leak the remote date when compressing HTTP Responses with gzip
* Its not a problem in TOR and its not a bug in the protocol as well and is not a problem with the GZIP
* It helps you get an idea of where one or another server is hosted.



### 5. favicon.ico matching

* favicon is that tiny icon that users see in the browser’s URL bar
* It is possible to match favicons found on dark web with favicons on the internet using Shodan
* The Quantum ransomware group is an example:

{% hint style="info" %}
Using its favicon from the dark web, Talos found its equivalent on the surface web and could locate the threat actor’s web server
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (218).png" alt=""><figcaption><p>favicon.ico matching</p></figcaption></figure>



### 6. Hacking the Server&#x20;

Find vulnerabilities in order to deanonymize the server

* Remote Command Execution
* Local File Inclusion
* Make a research on the server and look for other vulnerabilities that can leak the servers IP



### 7. Downgrading the HTTP Protocol

#### How to Find?

* Strange requests in my access.log file using HTTP/1.0 protocol:

```
"GET /NotFoundNotFoundNotFoundNotFoundNotFoundNotFou……….. HTTP/1.0" 400 802 "-"
"masscan - for more info go - http://something.org“
```

* Same behavior on my honeypots
* The requests keep coming for days
* I dumped the hole request
* I replicated and got an internal virtual host of mine that I didn’t want to be public
* This was the moment when I realized the potential of this flaw, both on the internet and dark web
* Started to develop an improved version of this /NoTFound…. request in order to exfiltrate the IP or unknown domains

#### Why this behavior?

* Is not because of a security problem in apache-based servers like: apache2, nginx or tomcat
* Is all about configuration
* The server must choose one of the domains to forward the request
* The client doesn’t supply a “**`Host: example.com`**“ header and to do that we can choose the first version of HTTP protocol -> HTTP/1.0
* The server will choose the first virtualhost
* In the response we can find first declared virtualhost. Which might be a domain or an IP or just localhost

#### The Leak

The leak is in the:

* **Triggered exceptions**
  * Doesn’t work on all apache-based servers
  * HTTP/1.0 400 Bad Request
  * HTTP/1.0 403 Forbidden
  * Even the 404 NotFound sometimes discloses the IP
* **Server redirects**
  * The best way to leak the IP
  * works in servers like nginx, apache2, tomcat

<figure><img src="../../../.gitbook/assets/image (219).png" alt=""><figcaption><p>Do not forget to downgrade</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (220).png" alt=""><figcaption><p>Do not forget to downgrade</p></figcaption></figure>



## 8. HTTP/1.0 400 Bad Request - Long Header

<figure><img src="../../../.gitbook/assets/image (221).png" alt=""><figcaption><p>Long Header</p></figcaption></figure>

* The same result with a long URL or a file upload that exceeds the server limit



### 9.  HTTP/1.0 403 Forbidden

* Very easy to trigger
* &#x20;I used the ^.ht\* rule and you can visit /.html to not attract attention
* The rule above is for .ht files, like .htacces or .htpasswd, etc

<figure><img src="../../../.gitbook/assets/image (222).png" alt=""><figcaption><p>403 Forbidden</p></figcaption></figure>



### 10.  Server Redirects

The best way to trigger redirect is to search for directories that serves static files

* servers based on apache must put a / at the end
* Exampe: if we visit http://server.com/dir it will auto redirect to http://server.com/dir/
* most cases you can find on the first page directories
* if there is an app without directories that serves something, then try some predefined directories that exists in some servers like “/img”, “/css”, “/icons”, “/js”
* this directories are available only if you visit with the IP 127.0.0.1, which most of the time in TOR this is the IP that you access the application

#### Trigger the Redirect

<figure><img src="../../../.gitbook/assets/image (223).png" alt=""><figcaption><p>Trigger the redirect</p></figcaption></figure>

#### Trigger the Redirect and Leak the IP

<figure><img src="../../../.gitbook/assets/image (224).png" alt=""><figcaption><p>Trigger the redirect to leak the IP</p></figcaption></figure>

{% hint style="info" %}
• I didn’t make a research on this. I suppose is at the limit of legality&#x20;

• It appears that others did this before, but I don't know if they followed this problem&#x20;

• I expect to exfiltrate domains that normally you cannot get from an IP. It's a kind of reverse DNS on a specific IP
{% endhint %}



### 11. Other Techniques - ETag

* The ETag or entity tag is part of HTTP, the protocol for the World Wide Web&#x20;
* Downgrade the protocol has nothing to do with this one &#x20;
* It suppose to take the ETag of the default domain and search it on the internet&#x20;
* We can find ETag in the response header&#x20;
* This can be done if the first page is static and not dynamic&#x20;
* We can use Shodan&#x20;
* The chance of success is quite small, but it's worth a try

#### Example of ETag

<figure><img src="../../../.gitbook/assets/image (225).png" alt=""><figcaption><p>Etag</p></figcaption></figure>



### 12. Other Techniques - Same Network Technique

* This technique involves domain enumeration on a given host&#x20;
* Because the number of known .onion address on TOR is small, then it is doable to search on the same server other TOR domains&#x20;
* If we find multiple domains on a single server then is enough to find the IP address of one of the domains to find the others&#x20;
* I remember I found a hosting provider on TOR for hidden services, but the owner didn’t used a good sandbox and I was able to find the IP address. Then if I would make a domain enumeration on that server I would find the other hidden services hosted on that server&#x20;
* To achieve that we need to change in “Host:” header the name of the hidden service with the ones from the list, one at a time and look for the response if is the same





***

## REFERENCES

* [https://dl.acm.org/doi/10.1145/3538969.3543808](https://dl.acm.org/doi/10.1145/3538969.3543808)
* [https://media.defcon.org/DEF%20CON%2030/DEF%20CON%2030%20presentations/Ionut%20Cernica%20-%20Deanonymization%20of%20TOR%20HTTP%20hidden%20services.pdf](https://media.defcon.org/DEF%20CON%2030/DEF%20CON%2030%20presentations/Ionut%20Cernica%20-%20Deanonymization%20of%20TOR%20HTTP%20hidden%20services.pdf)
* [https://www.youtube.com/watch?v=v45\_tkKCJ54](https://www.youtube.com/watch?v=v45\_tkKCJ54)
