---
icon: bars-progress
---

# Threat Hunting in Active Directory

## Auditing and Monitoring AD for Signs of Compromise



**Steps to Audit and Monitor Active Directory (AD)**

1.  **Enable Auditing in Active Directory:**

    * **How to Enable:**
      * Open the Group Policy Management console.
      * Navigate to the Default Domain Controllers Policy.
      * Right-click and select Edit.
      * Under Computer Configuration, expand Policies > Windows Settings > Security Settings > Advanced Audit Policy Configuration.\

    * **Audit Policies to Configure:**
      * **Account Logon**
      * **Account Management**
      * **Directory Service Access**
      * **Logon/Logoff**
      * **Object Access**
      * **Policy Change**\

    * **Tip:** Enable both success and failure events for comprehensive logging.

    \

2.  **Configure System Access Control Lists (SACLs):**\


    * **How to Configure:**
      * Open Active Directory Users and Computers.
      * Enable Advanced Features from the View menu.
      * Right-click on an object (e.g., user or group) and select Properties.
      * Go to the Security tab, click Advanced, then the Auditing tab.
      * Add a new auditing entry, select principal as everyone, and configure permissions to audit successful and failed attempts to read, write, and modify the object.


3. **Monitor Logs for Signs of Compromise:**\

   *   **Where to Monitor:**

       * Open Event Viewer and navigate to Windows Logs > Security.


   *   **Key Event IDs to Watch:**

       * **4625:** Failed log-on attempts (could indicate brute force attacks).
       * **4672:** Special privileges assigned to a new log-on (could indicate privilege escalation).
       * **4732 and 4733:** User added or removed from a security-enabled global group (could indicate unauthorized changes).


4.  **Use SIEM Tools for Streamlined Monitoring:**\


    * **Examples:** Microsoft Sentinel, Elastic SIEM, Splunk.
    * **Function:** Aggregate logs from multiple sources, correlate events, and generate alerts for suspicious activities.


5.  **Regularly Review Audit Logs and Alerts:**\


    * **Purpose:** Ensure auditing settings remain effective and no unauthorized changes have been made.



{% hint style="success" %}
By following these steps, you can effectively audit and monitor Active Directory for signs of compromise, helping to safeguard your network from malicious activity.
{% endhint %}



***

## Analyzing AD Logs and Events



**Analyzing Active Directory (AD) Logs and Events**

1.  **Primary Sources of Information:**

    * **Security System Logs:** Capture activities like user logins, changes in group memberships, and policy modifications.
    * **Directory Service Logs:** Found in the Event Viewer under Applications and Services Logs > Directory Service. These logs include events related to AD's internal operations.


2. **Key Event IDs to Monitor:**
   * **Event ID 2887:** Indicates whether LDAP traffic is being signed, crucial for preventing man-in-the-middle attacks.
   * **Event ID 2042:** Shows that replication has been stopped, which could lead to data inconsistencies.
   * **Event ID 1311:** Indicates problems with the AD replication process, potentially disrupting data synchronization.
   * **Event ID 1566:** Signifies that AD replication hasn't occurred for a significant period, suggesting network issues or configuration problems.
   * **Event ID 2040:** Indicates a mismatch in the AD schema, preventing updates to directory service objects.\

3. **Importance of These Events:**
   * **Replication Issues:** Can lead to inconsistencies in the AD database, which attackers might exploit to inject or delete malicious objects.
   * **Schema Mismatches:** Can cause operational issues and be exploited to bypass security controls.

\
**Key Takeaway:**&#x20;

The presence of these events doesn't necessarily mean an attack is happening but can help you form hypotheses for further analysis.\
\


{% hint style="success" %}
By understanding these logs and events, you can effectively monitor and identify potential threats in your AD environment.
{% endhint %}



***

## Uncovering Lateral Movement and Privilege Escalation



**Lateral Movement**

1.  **Definition:**

    * **Lateral Movement:** Techniques attackers use to move through a network after gaining initial access. This allows them to explore the environment, identify valuable assets, and escalate their privileges.


2.  **Common Scenario:**

    * **Initial Access:** An attacker gains access through a compromised user account.
    * **Tools Used:** Tools like Mimikatz are used to extract credentials from memory. Mimikatz can retrieve plain text passwords, hashes, and Kerberos tickets.


3. **Pass-the-Hash Technique:**
   * **Concept:** The attacker uses the NTLM hash of a user's password to authenticate without knowing the actual password.
   * **Tools:** SecSec or WMI can be used to execute commands on remote systems.\

4. **Example:**
   * **Event Viewer:** An extract from the Event Viewer in Windows shows a successful logon attempt.
   * **Key Fields:**
     * **Logon Type 3:** Refers to a network logon, such as accessing a shared resource over the network.
     * **Elevated Token:** Indicates that the logon session has elevated privileges.
     * **Security ID:** Contains the unique identifier for the account used.
     * **lsass.exe:** The Local Security Authority Subsystem Service, a critical system process responsible for enforcing security policy.

\
**Privilege Escalation**

1. **Definition:**
   * **Privilege Escalation:** Gaining higher-level permissions than initially granted, often by exploiting vulnerabilities or misconfigurations.\

2. **Common Methods:**
   * **Misconfigured Group Policy Objects (GPOs):** Attackers target GPOs or exploit vulnerabilities in services running with elevated privileges.
   * **JuicyPotato Exploit:** Used to gain system-level access on a Windows machine.\

3. **Example:**
   * **Event Viewer:** An event shows a fictitious user called compromised\_user logging on and being assigned special privileges.
   * **Key Privileges:**
     * **SeDebugPrivilege:** Allows debugging of processes.
     * **SeTakeOwnershipPrivilege:** Allows taking ownership of files and objects.

\
**Steps to Investigate Attacks:**

1. **For Lateral Movement:**
   * Check the source, network address, and workstation name to verify if the login attempt is legitimate.
   * Review recent activity for the admin account for unusual logon attempts or actions.
   * Investigate any unusual activity involving the lsass.exe process.
   * Analyze network traffic for unusual patterns or connections from the source address.\

2.  **For Privilege Escalation:**

    * Determine if the compromised user should have these privileges.
    * Check the account's normal role and responsibilities.
    * Look for other security events associated with this account.
    * Verify if the account was recently added to any privileged groups.
    * Check for changes to local or domain security policies.
    * Analyze network traffic to and from the target machine for suspicious activity.

    \


{% hint style="success" %}
By understanding these concepts and steps, you can better identify and respond to lateral movement and privilege escalation attempts in your Active Directory environment.
{% endhint %}



***

## Discover Common Kerberos Attack Techniques



**Kerberos and Kerberoasting Explained**\


1. **What is Kerberos?**
   * **Purpose:** Kerberos is a network authentication protocol used to verify the identity of users and services in a secure manner.
   * **Process:** When a user (like Alice) wants to access a resource (like an Excel workbook on a server), Kerberos assigns a ticket to the user, which is then used to authenticate and authorize access to the resource.\

2. **Kerberoasting Attack:**
   * **Concept:** An attacker tries to obtain a valid Kerberos ticket and crack its encryption to gain access to a user's password.
   * **Steps:**
     * **Initial Access:** The attacker must first gain access to the Active Directory (AD).
     * **Requesting Tickets:** The attacker requests Kerberos service tickets for accounts with ServicePrincipalName (SPN) attributes.
     * **Cracking Tickets:** The service tickets are encrypted with the hash of the service account's password. If the password is weak, the attacker can crack the ticket offline to retrieve the password.\

3. **Identifying Vulnerable Accounts:**

<figure><img src="../../.gitbook/assets/image (240).png" alt=""><figcaption><p>Powershell Script</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (241).png" alt=""><figcaption><p>Powershell Script</p></figcaption></figure>

* **PowerShell Script:** The script above explains a PowerShell script to identify accounts that are vulnerable to Kerberoasting.
  *   **Steps in the Script:**

      * Import the Active Directory module.
      * Check if the "don't expire password" flag is set.
      * Check if the user's password is stored using reversible encryption.
      * Retrieve all user accounts where the SPN attribute is not null.
      * Display properties like Name, SamAccountName, ServicePrincipalName, PasswordLastSet, and PasswordNeverExpires.
      * Format the output as a table and export to a CSV file for further analysis.



{% hint style="success" %}
By understanding these concepts and using the provided PowerShell script, you can identify and mitigate Kerberoasting vulnerabilities in your AD environment.
{% endhint %}



***

## Detect and Respond to Malicious GPO Activities



**Understanding Group Policy Objects (GPOs)**

1. **What are GPOs?**
   * **Definition:** Group Policy Objects are a powerful feature in Active Directory that allow administrators to manage and configure operating systems, applications, and user settings.
   * **Importance:** They help in organizing and enforcing policies across the network, making them a critical component of network management.\

2. **Why are GPOs a Target?**
   * **Attractiveness to Attackers:** Due to their powerful capabilities, GPOs are attractive targets for attackers looking to escalate privileges or deploy malicious configurations across the network.

\
**Detecting Malicious GPO Activities**

1.  **Key Events to Monitor:**

    * **Event ID 5136:** Indicates a GPO modification.
    * **Event ID 4670:** Signals a permission change on a GPO.


2. **Signs of Compromise:**
   * **Unusual Patterns:** Look for GPO changes made outside of normal administrative hours.
   * **Unauthorized Modifications:** Changes made by accounts that typically don't perform such actions.
   * **Deviation from Standards:** Modifications that deviate from your organization's standard configurations.
   * **New GPOs:** Be wary of new GPOs that appear without proper documentation or approval.

\
**Responding to Malicious GPO Activities**

1.  **Immediate Actions:**

    * **Isolate Affected Systems:** Prevent further spread of the compromise.
    * **Review and Revert Changes:** Revert any unauthorized modifications to the GPOs.
    * **Reset Passwords and Review Permissions:** Ensure that affected accounts are secure.


2. **Conduct a Thorough Investigation:**
   * **Scope of the Attack:** Understand the extent of the attack.
   * **Enhance Monitoring:** Improve your monitoring capabilities to detect future incidents.
   * **Regular Audits:** Conduct regular audits of GPO changes.
   * **Training:** Provide additional training for your administrative staff on security best practices.



{% hint style="success" %}
By understanding these key points, you can effectively detect and respond to malicious GPO activities, helping to protect your Active Directory domains from potential threats.
{% endhint %}

