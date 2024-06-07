# 9️⃣ A09:2021 – Security Logging and Monitoring Failures

## Security Logging and Monitoring Failures

Security logging and monitoring are crucial for detecting, escalating, and responding to active breaches. Without adequate logging and monitoring, security incidents may go undetected, leading to prolonged breaches and more significant damage.

## Characteristics of Security Logging and Monitoring Failures

*   **Insufficient Logging of Auditable Events**

    * **Description**: Failure to log important events like logins, failed logins, and high-value transactions.
    * **Example**: An application that does not log user login attempts.
    * **Impact**: Critical activities may go unnoticed, preventing timely detection of malicious actions.
    * **CWE-778: Insufficient Logging**: https://cwe.mitre.org/data/definitions/778.html


*   **Inadequate Log Messages for Warnings and Errors**

    * **Description**: Warnings and errors generate no, inadequate, or unclear log messages.
    * **Example**: A system that fails to log detailed error messages for failed login attempts.
    * **Impact**: Important warning signs of potential issues may be missed.
    * **CWE-223: Omission of Security-relevant Information**: https://cwe.mitre.org/data/definitions/223.html


*   **Unmonitored Application and API Logs**

    * **Description**: Logs of applications and APIs are not monitored for suspicious activity.
    * **Example**: API logs that are collected but never reviewed for anomalies.
    * **Impact**: Suspicious activities are not detected promptly, allowing attackers to exploit vulnerabilities longer.
    * **CWE-778: Insufficient Logging**: https://cwe.mitre.org/data/definitions/778.html


*   **Local-only Log Storage**

    * **Description**: Logs are only stored locally without centralized logging or off-site backups.
    * **Example**: Storing logs on the same server as the application, risking loss if the server is compromised.
    * **Impact**: Log data can be easily tampered with or lost, impeding forensic investigations.
    * **CWE-257: Storing Passwords in a Recoverable Format**: https://cwe.mitre.org/data/definitions/257.html


*   **Lack of Alerting and Escalation Processes**

    * **Description**: Inadequate alerting thresholds and response escalation processes.
    * **Example**: No alerts set up for multiple failed login attempts, missing potential brute force attacks.
    * **Impact**: Delays in responding to active attacks, increasing potential damage.
    * **CWE-1009: Failure to Enable Notification Mechanism**: https://cwe.mitre.org/data/definitions/1009.html


*   **Penetration Testing and DAST Scans Not Triggering Alerts**

    * **Description**: Penetration testing and scans by DAST tools do not trigger alerts.
    * **Example**: DAST scans conducted without triggering any alerts or notifications to the security team.
    * **Impact**: Security testing activities go unnoticed, potentially missing opportunities for improvement.
    * **CWE-778: Insufficient Logging**: https://cwe.mitre.org/data/definitions/778.html


*   **Inability to Detect or Escalate Active Attacks**

    * **Description**: The application cannot detect, escalate, or alert for active attacks in real-time or near real-time.
    * **Example**: Real-time monitoring systems are not in place, missing ongoing attacks.
    * **Impact**: Active attacks remain undetected, leading to prolonged breaches.
    * **CWE-1008: Sensitive Data Exposure Through Discrepancy**: https://cwe.mitre.org/data/definitions/1008.html


* **Information Leakage in Logs**
  * **Description**: Logging and alerting events visible to users or attackers.
  * **Example**: Error messages with sensitive information shown to users.
  * **Impact**: Attackers gain insight into system internals, aiding further attacks.
  * **CWE-532: Information Exposure Through Log Files**: https://cwe.mitre.org/data/definitions/532.html

## Prevention

*   **Log Critical Events**:

    * Log all login attempts, access control failures, and server-side input validation failures with sufficient user context for forensic analysis.


*   **Format Logs for Compatibility**:

    * Generate logs in a format that can be easily consumed by log management solutions.


*   **Secure Log Data**:

    * Encode log data correctly to prevent injection attacks on logging or monitoring systems.


*   **Audit Trails for High-Value Transactions**:

    * Maintain an audit trail for high-value transactions with integrity controls to prevent tampering or deletion.


*   **Implement Effective Monitoring and Alerting**:

    * Establish monitoring and alerting systems to detect and respond to suspicious activities promptly.


*   **Incident Response and Recovery Plan**:

    * Develop and adopt an incident response and recovery plan, such as NIST 800-61r2 or later.


* **Use Protection Frameworks and Tools**:
  * Utilize application protection frameworks (e.g., OWASP ModSecurity Core Rule Set) and log correlation software (e.g., ELK stack) for custom dashboards and alerting.



***

## References

* [OWASP Proactive Controls: Implement Logging and Monitoring](https://owasp.org/www-project-proactive-controls/v3/en/c9-security-logging.html)
* [OWASP Application Security Verification Standard: V7 Logging and Monitoring](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Testing Guide: Testing for Detailed Error Code](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web\_Application\_Security\_Testing/08-Testing\_for\_Error\_Handling/01-Testing\_for\_Error\_Code)
* [OWASP Cheat Sheet: Application Logging Vocabulary](https://cheatsheetseries.owasp.org/cheatsheets/Application\_Logging\_Vocabulary\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Logging](https://cheatsheetseries.owasp.org/cheatsheets/Logging\_Cheat\_Sheet.html)
* [Data Integrity: Recovering from Ransomware and Other Destructive Events](https://csrc.nist.gov/publications/detail/sp/1800-11/final)
* [Data Integrity: Identifying and Protecting Assets Against Ransomware and Other Destructive Events](https://csrc.nist.gov/publications/detail/sp/1800-25/final)
* [Data Integrity: Detecting and Responding to Ransomware and Other Destructive Events](https://csrc.nist.gov/publications/detail/sp/1800-26/final)
* [https://owasp.org/Top10/A09\_2021-Security\_Logging\_and\_Monitoring\_Failures/](https://owasp.org/Top10/A09\_2021-Security\_Logging\_and\_Monitoring\_Failures/)

## Mapped CWEs

* [CWE-117 Improper Output Neutralization for Logs](https://cwe.mitre.org/data/definitions/117.html)
* [CWE-223 Omission of Security-relevant Information](https://cwe.mitre.org/data/definitions/223.html)
* [CWE-532 Insertion of Sensitive Information into Log File](https://cwe.mitre.org/data/definitions/532.html)
* [CWE-778 Insufficient Logging](https://cwe.mitre.org/data/definitions/778.html)
