---
icon: atom-simple
---

# Protocols

## HTTP Protocol

### HTTP Vs. HTTPS

* **HTTP (Hypertext Transfer Protocol):**
  * An older protocol used for transferring data over the web.
  * Data is sent in plain text, making it readable by anyone who intercepts it.\

*   **HTTPS (Hypertext Transfer Protocol Secure):**

    * An encrypted version of HTTP.
    * Protects data in transit, making it secure from eavesdropping.



### Why HTTP is Still Relevent

*   Although most of the internet now uses HTTPS, some servers still use HTTP. These include:

    * Old informational websites.
    * Organizations that can't afford digital certificates.
    * Testing or development servers.
    * Network devices like switches and routers.



### Key Characteristics to Examine in HTTP Traffic

1.  **User Agent Strings:**

    * Part of the HTTP header that provides information about the client's software (e.g., browser, operating system).
    * **Hunting Approach:** Establish a baseline of common user agents (like Chrome, Firefox) and look for unusual ones (e.g., bots, malware).


2.  **URIs (Uniform Resource Identifiers):**

    * Strings used to identify resources on a server.
    * **Hunting Approach:** Look for long, random-looking URIs or those with high entropy (randomness).


3.  **HTTP POST Requests:**

    * Used to send data to a server (e.g., logging in, submitting forms).
    * **Hunting Approach:** High volume of POST requests to the same website can indicate data exfiltration or command and control activity.


4. **Host Names:**
   * Specifies the domain name or IP address of the web server.
   * **Hunting Approach:** Look for recently registered domains, suspicious top-level domains (e.g., .tk, .cn), or IP addresses instead of domain names.

### Geographic Information

* **GeoIP Information:**
  * Identifying the geographic location of web servers.
  * **Hunting Approach:** Determine if traffic is going to unexpected locations. For example, a dentist's office in Los Angeles seeing traffic to China might be suspicious.\


### Practical Application

* **Baseline:** Establish what is normal in your network (common user agents, typical URIs, regular POST requests).
* **Analyze:** Look for deviations from this baseline to identify potential threats.
* **Collaborate:** Work with IT to get a list of authorized systems and software to speed up the process.

By focusing on these key areas, you can effectively hunt for malicious activity in HTTP traffic and protect your network from potential threats.



## HTTPS Protocol

### HTTPS Overview

**HTTPS (Hypertext Transfer Protocol Secure):**

* A secure extension of HTTP.
* Provides an encrypted connection between the client (e.g., web browser) and the web server.
* Protects data during transit, making it secure from eavesdropping.

### Challenges with HTTPS in Threat Hunting

**Encryption Limits Visibility:**

* HTTPS hides valuable fields such as User-Agent string, hostname, request method, and the body of the HTTP message.
* This makes it harder to inspect traffic for threat hunting.

### How to Hunt for Malicious HTTPS Traffic

1.  **Intercepting HTTPS Traffic:**

    * HTTPS traffic can be intercepted and proxied by an IT department or security team.
    * Requires pre-configuration on the network to inspect the content of HTTPS packets.


2. **Analyzing Metadata:**
   * Even though the content is encrypted, some metadata can still be analyzed to identify suspicious traffic.
   * **Analogy:** Think of HTTPS traffic like a discrete package. While the contents are hidden, you can still observe the sender's and recipient's addresses, size, weight, etc.

### Key Metadata to Analyze

1.  **Server Name Indication (SNI):**

    * Part of the TLS handshake where the client specifies the domain name it is trying to reach.
    * Helps identify communication to and from suspicious websites.
    * **Example:** During a hunt, you can carve out SNIs and use techniques like least frequency of occurrence to identify potentially malicious interactions.


2. **Distinguished Name (DN):**
   * Contains values like country, city, state, organization name, issuer, and domain name.
   * **Focus on Issuer:** Look for free, inexpensive, and untrusted issuers (e.g., Let's Encrypt) as threat actors often use these for malicious purposes.

### Practical Steps

**Using Tools:**

* Tools like Wireshark or Zeek can help locate the server name and issuer in HTTPS traffic.



By focusing on these aspects, you can effectively hunt for malicious HTTPS traffic despite the encryption, enhancing your network security efforts.



## SMB Protocol

* **SMB Protocol Usage:** SMB (Server Message Block) is used for sharing files on a network, commonly found in Windows environments. It uses TCP port 445 for communication.
* **Threat Actor Techniques:** Threat actors use SMB for running commands, searching for sensitive information, and moving through networks. Notable attacks like NotPetya and the SolarWinds compromise have leveraged SMB.
* **Detection Challenges:** Malicious SMB activity often blends in with regular file sharing, making it hard to detect. However, analyzing SMB metadata such as Command and Filename in tools like Wireshark and Zeek can help identify suspicious activities.

\
By understanding these points, you can better recognize and respond to potential threats using the SMB protocol.



## DNS Protocol

### DNS Overview

**DNS (Domain Name System):**

* Translates human-friendly domain names (like linkedin.com) into machine-readable IP addresses.
* Functions like a phone book for the internet, allowing users to look up websites by their names.

### Types of DNS Records

* **A Records:** Contain IPv4 addresses.
* **Quad A Records:** Contain IPv6 addresses.
* **CNAME Records:** Redirect one domain or subdomain to another.
* **MX Records:** Specify where emails should be routed.
* **NS Records:** Store the name server for a DNS entry.
* **TXT Records:** Contain textual notes.

### Security Enhancements

* **DNS over HTTPS (DoH):**
  * Introduced in 2017 by the Internet Engineering Task Force (IETF).
  * Encrypts DNS queries to enhance security and privacy.
  * Supported by major web browsers and DNS providers.

### Hunting for Malicious DNS Activity

1.  **Uncommon Resource Record Types:**

    * Look for hosts with a high volume of uncommon record types (e.g., TXT records).
    * Attackers may use these for command and control channels.


2.  **Uncommon Top-Level Domains:**

    * Hunt for domains with unusual top-level domains (e.g., .XYZ, .iso).
    * These can be used by threat actors to evade detection.


3.  **Geographic Indicators:**

    * Hunt for top-level domains indicating regions where your organization doesn't usually operate (e.g., .CN, .UK).


4.  **High Volume of Subdomains:**

    * Look for a high volume of subdomains under a single parent domain.
    * Attackers might use subdomains for data exfiltration or command and control instructions.


5.  **Long or High Entropy Domain Names**

    * Hunt for very long or unreadable domain names.
    * These could be signs of domain generation algorithms (DGAs).


6.  **Newly Registered or Recently Changed Domains:**

    * Hunt for domains that are newly registered or have recent ownership changes.
    * These may be associated with malicious activity.


7. **Doppelganger Domains:**

* Look for domains that resemble your own but have slight differences (e.g., LinkedIn without the "i" - "Linkedn.com").
* These are often used for phishing attacks.



## Practical Application

**Adjust Network Configurations:**

* For better visibility into DNS queries, you may need to adjust network configurations.
* It's no longer as simple as capturing packets on your firewall.

By focusing on these aspects, you can effectively hunt for malicious DNS activity and enhance your network security efforts.
