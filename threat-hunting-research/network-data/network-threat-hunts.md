---
icon: calendar-users
---

# Network Threat Hunts

## Hunt Command and Control (C2)

### Command and Control Server Overview

**C2 Servers:**

* Think of a C2 server like a conductor of an orchestra. Just as a conductor instructs musicians on when and how to play, a C2 server issues commands to compromised devices, specifying actions and timing.
* Once an adversary gains access to a network, they use a C2 server to maintain that access and control the compromised devices.

### C2 Communication Methods

1.  **Common Protocol on a Common Port:**

    * Attackers use standard protocols like HTTPS on common ports to blend in with regular network traffic.
    * Example: Cozy Bear used HTTPS to hide malicious traffic within normal web traffic.


2. **Custom Protocol on a Standard Port:**
   * Attackers might use custom protocols on standard ports to avoid detection.
   * Example: Fake malware used a modified SSL implementation on common ports like 80, 443, and 53.\

3. **Common Protocol on an Uncommon Port:**
   * Using standard protocols on uncommon ports makes the traffic stand out.
   * Example: Using DNS or HTTPS on an unusual port like 2222.

\
4\. **Custom Protocol on an Uncommon Port:**

* Attackers use custom protocols on rarely used ports to evade detection.
* Example: The Cryptic Malware Family used custom protocols on uncommon ports.

### Hunting for C2

*   **Identify Communication Patterns:**

    * Look for consistent intervals in connections, such as a device checking in with the same IP address every 60 seconds.
    * Investigate persistent connections, which can indicate an open line of communication with the compromised system.


*   **Tools and Techniques:**

    * Use threat intelligence feeds to identify known C2 indicators of compromise (IOCs).
    * Tools like Wireshark and Zeek can help analyze network traffic and identify top talkers (frequent communication pairs).


*   **Handling Sophisticated Techniques:**

    * Some attackers use jitter (variable check-in times) to avoid detection. Analyze network data over a long period to identify average check-in intervals.



By understanding these concepts, you can better recognize and respond to potential C2 activities on your network. This knowledge is crucial for effective threat hunting and maintaining network security.



## Hunt Lateral Movement

### Lateral Movement Overview

**Definition:**

* Lateral movement refers to the techniques attackers use to move from one system or endpoint to another within a network after gaining initial access.
* The goal is to explore the network, escalate privileges, access sensitive data, and establish a persistent presence while remaining undetected.

### Methods of Lateral Movement

1.  **Exploitation of Vulnerabilities:**

    * Attackers exploit unpatched vulnerabilities in software or systems to move laterally.
    * **Example:** Using a known vulnerability in an outdated application to gain access to another system.


2.  **Using Stolen Credentials:**

    * Attackers use stolen usernames and passwords to log into other systems within the network.
    * **Example:** Harvesting credentials through phishing attacks or keyloggers.


3. **Leveraging Legitimate Tools and Protocols:**

Attackers use legitimate tools and protocols to blend in with normal network activity.

* **Examples:**
  * **SMB (Server Message Block):** Used for file sharing and can be exploited for lateral movement.
  * **RMM (Remote Management Tools):** Tools like Remote Desktop Protocol (RDP) or SSH.
  * **Native System Tools:** Tools like FTP (File Transfer Protocol) and SCP (Secure Copy Protocol).\


### Strategies for Hunting Lateral Movement

1.  **Monitoring Failed Login Attempts:**

    * Keep an eye on repeated failed login attempts, which may indicate an attacker trying to use stolen credentials.


2.  **Remote Management Tool Usage:**

    * Watch for unusual or unauthorized use of remote management tools.


3.  **Lateral Tool Transfer:**

    * Monitor for the transfer of tools via SMB, RMM tools, or native system tools like FTP and SCP.


4.  **Cloud Services and File Storage:**

    * Pay attention to the use of cloud services or cloud file storage (e.g., Dropbox) for unusual activity.


5.  **Software Deployment Tools:**

    * Look for suspicious use of software deployment tools like SCCM (System Center Configuration Manager).


6.  **Tainted Shared Content:**

    * Be cautious about shared content on SMB file shares that may be compromised.


7. **Living-off-the-land Binaries:**
   * Monitor the use of legitimate system binaries like PsExec, which attackers can use to move laterally.

### Key Takeway

* By staying vigilant and knowing what to look for, you can significantly reduce the likelihood of successful lateral movement within your network. A well-informed and proactive defense is your strongest asset against evolving cyber threats.

\
Understanding these concepts will help you better recognize and respond to potential lateral movement activities, enhancing your network security efforts.



## Hunt Remote Desktop Software

### Background

* **Remote Management and Monitoring (RMM) Tools:**
  * These tools allow IT professionals to manage and monitor workstations and servers remotely.
  * They provide functionalities like deploying software, enforcing security settings, troubleshooting issues, and logging into customer endpoints.

### Key Points

**Adversaries' Use of RMM Tools:**

* Just as IT professionals use RMM tools for convenience, adversaries also see their value.
* Attackers use legitimate RMM tools to evade detection and blend into the network.
* They can gain access to sensitive data, initiate ransomware attacks, or perform other malicious activities.

**Common RMM Tools Used by Adversaries:**

* **AnyDesk:** The most frequently used RMM tool in intrusions.
* **Other Tools:** ConnectWise ScreenConnect, Atera, TeamViewer, Remote Desktop Plus, RustDesk, Splashtop, FleetDeck, TightVNC, and N-able remote access software.

### Hunting RMM Tools

1. **Authorized Tools and Users:**
   * Start by identifying which RMM tools are authorized and who is expected to use them.
   * Look for outliers or unauthorized usage.\

2.  **Endpoint Telemetry:**

    * If you have access to endpoint telemetry (like EDR tools or Sysmon), set up alerts for process creation events where RMM binaries are executed.
    * Monitor for tools like AnyDesk, RustDesk, or TightVNC being used.


3. **Network Indicators:**

* If endpoint telemetry is not available, look for network indicators:
  *   **Port Numbers:**

      * TeamViewer: TCP/UDP port 5938, TCP port 443, TCP port 80.
      * TightVNC: TCP ports 5800-5900.
      * Microsoft Remote Desktop: Port 3389.


  * **Domain Names:**
    * N-able remote desktop: n-able.com.
    * TeamViewer: teamviewer.com.

4. **Grouping and Session Length:**

* Group business units (e.g., finance, HR) and identify unusual patterns in remote desktop usage.
* Analyze session lengths to find outliers. For example, short sessions in an environment where long sessions are common might indicate suspicious activity.

5. **High Number of Connections:**

* Look for users or systems initiating a high number of remote desktop sessions.
* Most users won't log into more than one system, but adversaries might attempt to log into many systems to move laterally.

### Key Takeaway

**Double-Edged Sword:**

* RMM tools offer both convenience and risk. By being vigilant and implementing strategies to hunt for unauthorized RMM usage, you can protect your network.



Understanding these concepts will help you better recognize and respond to potential threats using remote desktop software, enhancing your network security efforts.\




