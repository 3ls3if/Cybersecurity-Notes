---
icon: toolbox
---

# Network Threat Hunting Too

## SIEM for Threat Hunting

* **SIEM (Security Information and Event Management)**: Think of SIEM as a central security control room that collects and analyzes log data from various parts of your network.\

* **Log Data**: This includes information from firewalls, routers, DNS, endpoint logs, and more. It's like gathering clues from different sources to solve a mystery.

**Key Functions of SIEM**:

* **Indicator Search**: Searching for specific signs of compromise, like looking for known bad IP addresses or domain names.
* **Stack Counting**: Counting how often certain events happen to spot anything unusual.
* **Clustering**: Grouping similar data points to find patterns.
* **Ratios**: Comparing different values, like the number of login attempts versus successful logins.
* **Standard Deviation**: Finding outliers by seeing how much data deviates from the average.

**Example Scenario**: Imagine you're a detective. You notice an unusual amount of remote desktop traffic on a specific system. By using SIEM, you can trace back to see failed login attempts, identify the source, and find a suspicious email that might have caused the issue. This helps you quickly isolate the problem and prevent further damage.



## Wireshark for Threat Hunting

* **Wireshark**: It's a free, open-source tool used for analyzing network packets. Think of it as a magnifying glass that lets you see the details of data traveling over your network.\

* **Packet Analysis**: Wireshark captures and analyzes packets (small chunks of data) sent over the network. Imagine trying to read 185 lines of text per second; Wireshark helps you make sense of this by organizing and visualizing the data.\

* **Protocol Dissectors**: These are like translators for different network protocols (rules for data exchange). They break down packets into understandable parts, allowing you to create filters to focus on specific types of traffic. For example, you can filter HTTP packets to see only those with an IP address instead of a domain name.



* **Configuration Profiles**: These are customizable views in Wireshark. You can switch between different profiles based on what you're looking for. For instance, you might have one profile for DNS traffic and another for HTTP traffic, each with tailored filters and columns.\

* **Protocol Hierarchy**: This feature shows a tree view of all protocols in the captured data, with statistical values for each. It's like a summary that helps you narrow down your focus. If you see a lot of SMB traffic, you can switch to analyzing that specific protocol.\

* **Endpoint Statistics**: This feature lets you see conversations between two endpoints (devices) on the network. It's useful for identifying which devices are communicating the most, helping you spot unusual activity.\


## IDS or IPS for Threat Hunting

### IDS

<figure><img src="../../.gitbook/assets/image (237).png" alt=""><figcaption></figcaption></figure>

* **Purpose**: IDS is designed to monitor and analyze network activity to detect potential threats. It alerts security administrators when suspicious activity is detected but does not block the activity.

**Types**:

* **Network-based IDS (NIDS)**: Monitors network traffic in real-time, examining packets as they move across the network. It uses techniques like signature-based detection (matching known attack patterns) and anomaly-based detection (identifying deviations from normal behavior).
* **Host-based IDS (HIDS)**: Installed on individual machines or servers, monitoring activity on the host itself.

### IPS

<figure><img src="../../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

* **Purpose**: IPS not only detects potential threats but also takes action to prevent or block them. It can be configured to either detect or block suspicious activity, depending on the organization's needs.
* **Example**: If an IPS detects a known malware signature, it can automatically block the traffic to prevent the malware from spreading.

### Key Differences

* **Detection vs. Prevention**: IDS focuses on detecting and alerting about threats, while IPS takes it a step further by actively preventing threats.
* **Placement**: NIDS can be placed at strategic points within a network to monitor traffic, while HIDS is installed on individual hosts.

### Practical Application

* **Example Scenario**: Suppose you're hunting for unauthorized web servers on your network. You might use an IDS like Snort to create rules that alert you when certain suspicious HTTP traffic is detected. For instance, you can set a rule to alert you when HTTP traffic contains cleartext passwords, which could indicate a potential threat.

### Snort Rule Breakdown

<figure><img src="../../.gitbook/assets/image (238).png" alt=""><figcaption><p>Snort Rule to Detect Malicious HTTP Traffic</p></figcaption></figure>

* **Alert**: Specifies the action to be taken when the condition is met.
* **TCP**: Specifies the network protocol.
* **$HOME\_NET any**: Indicates any source port for devices in the protected network.
* **$EXTERNAL\_NET**: Represents external or untrusted networks.
* **$HTTP\_PORTS**: Defines ports used for web traffic.
* **Content Filters**: Checks for specific HTTP methods (e.g., GET) and paths (e.g., /malicious-path).
* **SID**: Unique identifier for the rule.



## Bro or Zeek for Threat Hunting

In your role, you can use Zeek to enhance your network security monitoring. Zeek provides detailed logs that go beyond basic network flow data, offering insights into HTTP sessions, DNS requests, SSL certificates, and more. This allows you to:

* **Detect Anomalies**: By analyzing Zeek logs, you can identify unusual patterns, such as a file disguised as an image but actually being an executable, which could indicate malware.
* **Identify Threats**: Use Zeek to spot signs of drive-by compromises by focusing on download activity from external websites and examining HTTP logs for suspicious MIME types.
* **Monitor Network Activity**: Zeek helps you track various network activities, such as SSH brute force attacks and SSL certificate validation, providing a comprehensive view of potential threats.

By leveraging Zeek's capabilities, you can proactively hunt for threats and improve your organization's overall security posture.



**Zeek Overview**:

* Originally known as Bro, developed in the 1990s.
* Open-source network security monitoring tool.
* Provides real-time analysis of network traffic to detect anomalies and security threats.

**Key Features**:

*   **Detailed Logs**: Offers application layer transcripts, unlike basic network flow data.

    * Logs include HTTP sessions, requested URIs, key headers, MIME types, server responses, DNS requests, SSL certificates, etc.



    * **Built-in Capabilities**:
      * Extract files from HTTP sessions.
      * Identify malware through external registries.
      * Report on vulnerable software versions.
      * Detect SSH brute force attacks.
      * Validate SSL certificate chains.



**Advantages**:

* Provides deeper insights compared to network flow data.
* Enhances visibility without excessive storage demands.



**Practical Application**:

* **Initial Access Detection**:\

  * Focus on download activity from external websites.
  * Examine HTTP logs where the `RESP_FUIDS` field is not empty (indicates file transfers).
  * Use MIME types field to identify potential threats (e.g., files disguised as images but are executables).

**Example**:

* Identified malware by noticing a file named `a.png` was actually an executable through MIME types field in Zeek logs.



**Conclusion**:

* Zeek is a valuable tool for network security monitoring, helping to uncover and respond to a wide range of potential threats.



## Security Onion

**Overview**:

* Security Onion is an open-source network security monitoring and threat hunting operating system.
* Created by Doug Burks.
* Comparable to Kali Linux but for blue teams (defensive security).

**Included Tools**:

* **Strelka**: Real-time file scanning.
* **Suricata**: Signature-based detection.
* **Zeek**: Rich network protocol metadata.
* **CyberChef**: Code analysis.
* **OpenCanary**: Honeypots.
* **Elastic Stack**: Centralized management.

**Benefits**:

* Simplifies the setup, deployment, and management of blue team tools.
* Consolidates multiple powerful security tools into a single platform.
* Enhances threat hunting efficiency by providing a versatile toolkit.

**Practical Application**:

* Can be deployed on the network to collect and analyze traffic in real-time.
* Can import full packet capture files or Windows event logs for analysis.
* Example: Used to detect an NMAP OS detection probe, leading to the discovery of a suspicious file download and decoding it to reveal a web shell.

**Analogy**:

* Compared to a well-stocked kitchen with various tools, making the threat hunting process faster and more efficient.
