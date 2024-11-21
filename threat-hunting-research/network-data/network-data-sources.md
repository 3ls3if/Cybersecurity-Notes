---
icon: globe
---

# Network Data Sources

## Network Threat Hunting Data Sources

* **Network Data Sources**: These are the different types of data you can use to look for signs of malicious activity on a network.
* **Full Packets**: Think of this as capturing every detail of a conversation happening over the network, like recording a phone call.
* **NetFlow or sFlow**: This is more like a summary of the network traffic, similar to a phone bill that shows who called whom and for how long, but not the content of the conversation.
* **Infrastructure Logs**: These are records of events or activities from network devices, like a diary of what happened on your firewall or server.

## Threat Hunting in Packets

* **Packets**: When data is sent over the internet, it is broken down into smaller pieces called packets. Think of it like sending a book through the mail by dividing it into smaller envelopes. Each envelope contains a part of the book, and the receiver puts them back together to read the full book.
* **Packet Capture**: Capturing packets is like having surveillance cameras on your network. You can see all the data coming in and going out. This helps in identifying any suspicious activity.
* **Storage**: Storing all these packets can be expensive because it requires a lot of space, especially for large networks.
* **Visibility**: Capturing packets at the network's entry and exit points (like the main gate of a building) gives you a good view of what's coming in and going out but doesn't show you movement within the network (like inside the building).
* **Encryption**: Modern networks often use encryption to protect data, which can make it harder to see the contents of packets without special setup.\


## Threat Hunting Using Network Flow Data

*   **Network Flow Data**: Think of network flow data as a summary of network activity. It's like looking at a phone bill that shows who called whom, when, and for how long, but not the actual conversation. It includes:

    * **Source and Destination Addresses**: Where the data is coming from and going to.
    * **Port Numbers**: Which application or service is sending or receiving data (e.g., web traffic uses port 80 for HTTP).
    * **Timestamps**: When each data packet or network connection started and ended.
    * **Packet and Byte Counts**: How many data packets and bytes are being sent.
    * **Protocol Information**: Which network protocols are being used (e.g., TCP or UDP).
    * **Flow Direction**: Whether the traffic is inbound (coming into the network) or outbound (leaving the network).


*   **Advantages of Network Flow Data**:

    * **Small Data Size**: Easier to store and analyze compared to full packet captures.
    * **Privacy**: Only metadata is captured, not the actual content of the data packets.


* **Challenges**:
  * **Validation**: It can be difficult to confirm findings using network flow data alone. For example, normal activities like LDAP lookups or Kerberos authentication can look like a DDoS attack.

\
**Use Cases**: Network flow data is useful for identifying abnormal network traffic patterns, behavioral analysis, command and control detection, and data exfiltration hunting. It allows you to quickly scan large amounts of data and then focus on specific areas if needed.



## Threat Hunting  in Infrastructure Logs

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Infrastructure Logs**: These are records of activities and events from various hardware and software in an IT environment, like routers, switches, firewalls, and endpoints. Think of them as a diary that notes everything happening in your network.\
  \

*   **Types of Logs**:

    * **Proxy Logs**: These logs capture web browsing data, including outgoing web requests and encrypted HTTPS traffic.
    * **DNS Logs**: These logs record domain resolution activities, showing which domains are being requested by devices in your network.
    * **Firewall and Router Logs**: These logs track data coming into and going out of your network (north-south traffic) and data moving within your network (east-west traffic).



**Using Logs for Threat Hunting**:

* **HTTP User Agents**: Look for unusual user agents in proxy logs to catch unwanted activity. Hacking tools often have default user agent strings that can be detected.
* **Large Data Transfers**: Firewall logs can reveal large files being transferred, which might be suspicious if done by unexpected users.
* **Command and Control Channels**: Attackers use domain generation algorithms (DGAs) to create domains for their control channels. These domains look random and can be detected in DNS logs.
