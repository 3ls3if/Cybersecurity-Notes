---
icon: user-secret
---

# Hunting the Undetected

## IOCs in Threat Hunting

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

**Pyramid of Pain:**

* The Pyramid of Pain is a model that helps understand how difficult it is for attackers to avoid detection.
* It has different levels, starting from the easiest to the hardest for defenders to detect.



**Levels of the Pyramid:**

1. **Hashes:**
   * Think of hashes like unique fingerprints for files. They are easy to search for and detect because they are unique.
2. **IP Addresses:**
   * These are like phone numbers for computers. They are also easy to search for but can change over time.
3. **Domain Names:**
   * These are website names. They are simple to find but attackers can easily change them.
4. **Network and Host Artifacts:**
   * These include patterns in network traffic or specific file behaviors. They are more complex and harder to detect.
5. **Tools:**
   * These are the software tools attackers use. Detecting these is challenging because attackers can change or replace them.
6.  **Tactics, Techniques, and Procedures (TTPs):**

    * These are the specific methods and behaviors attackers use. They are the hardest to detect but provide the most valuable information.



**Key Takeaway:**

* The higher up the pyramid, the harder it is for attackers to avoid detection, but it also becomes more challenging for defenders to detect these indicators.



**Application:**

* To improve threat hunting, start with the easier indicators (like hashes and IP addresses) and gradually work towards detecting more complex behaviors (like TTPs).



## Baseline to Identify Anomalies

* **Baselining:** Establishing what is considered normal within a network by analyzing historical data, traffic patterns, system behaviors, and user activities. This helps in identifying anomalies and potential security threats.
* **Advantages:**
  * Familiarizes you with new datasets or environments.
  * Reduces false positives by filtering out known benign activities.

**Disadvantages:**

* Existing intrusions might be considered normal if they are part of the baseline.
* It takes time to establish a reliable baseline.

By regularly conducting threat hunts based on these baselines, you can proactively identify potential threats and protect your organization from cyber attacks.



## Least Frequency Analysis to Identify Outliers

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Least Frequency Analysis (LFO):** This technique helps in spotting unusual or rare items in large sets of data. It focuses on finding things that appear the least often, as these are more likely to be suspicious.\
  \

* **How It Works:** Imagine you have a list of items that show up in your network. Most common items are usually safe and appear frequently. Least frequency analysis brings the rare items to the forefront, making it easier to spot potential threats.



* **Example:** Think of it like looking at a crowd of people. Most people are wearing common clothes, but if you see someone in a unique costume, they stand out. Similarly, in network data, the rare items (like unusual files or activities) stand out and are worth investigating.\
  \

* **Application:** This method can be used to analyze various data points like user agents, network ports, DNS queries, and payload sizes to identify anomalies and potential threats.



By focusing on the least common occurrences, you can efficiently sift through large data sets and pinpoint potential security threats that might otherwise go unnoticed.



## Hypothesis Threat Hunting

* **Definition:** Hypothesis threat hunting involves creating educated guesses (hypotheses) about potential threats in your network and then testing these hypotheses to see if they hold true.

### Steps to Create a Hypothesis

1. **Read Industry Reports and Research Papers:**\

   * Gain insights from trusted sources like industry reports, research papers, blogs, or social media updates from thought leaders. These sources provide valuable information on current threats and trends.\

2.  **Use Mind Maps:**\


    * Start with a central idea and brainstorm related topics by creating branches. This helps in generating new ideas and exploring different angles.


3. **10 Ideas in 10 Minutes:**
   1. Set a timer and aim to come up with at least 10 ideas in 10 minutes. This technique encourages creativity and helps overcome the fear of not having the perfect idea.

### Example Hypothesis

1.  **PowerShell Abuse:**

    * After reading a report about an increase in malware-free attacks using PowerShell, you might hypothesize that PowerShell is being used for malicious activities in your network. You can then focus on HTTP traffic where the user agent string contains "PowerShell."


2.  **Geopolitical Events:**

    * During a geopolitical event, you might hypothesize that affected individuals or organizations could target banks. You can then review threat intelligence data to identify common malware and techniques from the region of concern.


3. **Phishing Campaigns:**
   * After reading about a correlation between corporate mergers and phishing attacks, you might hypothesize that companies undergoing mergers are more likely to be targeted. You can then initiate threat hunts to detect phishing campaigns and malicious links.

### Key Takeways

* **Creativity:** Be creative in forming hypotheses. Use various techniques like reading reports, mind mapping, and brainstorming.
* **Testing:** Once you have a hypothesis, identify the data sources needed to test it and look for evidence to support or refute it.
* **Adaptability:** Adjust your hypotheses based on new information and continuously refine your threat-hunting strategies.

By following these steps, you can proactively identify and mitigate potential threats in your network.

