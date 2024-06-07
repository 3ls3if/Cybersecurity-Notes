# 5️⃣ A05:2021 – Security Misconfiguration

## Security Misconfiguration

Security misconfiguration refers to the improper implementation or insufficient configuration of security controls across any part of the application stack. This can lead to vulnerabilities that expose the application to various attacks. Misconfiguration can occur at different levels, including servers, databases, frameworks, and application settings.

## Characteristics of Security Misconfiguration Vulnerabilities

*   **Missing Appropriate Security Hardening**

    * **Description**: Security hardening is not implemented across the application stack, leading to potential vulnerabilities.
    * **Example**: An application server running with default settings and unnecessary services enabled.
    * **Impact**: Attackers can exploit these services to gain unauthorized access or disrupt the application.


*   **Unnecessary Features Enabled**

    * **Description**: Unnecessary ports, services, pages, accounts, or privileges are enabled or installed.
    * **Example**: A database server has unused ports open, allowing attackers to connect to it.
    * **Impact**: Attackers can leverage these unused ports to exploit vulnerabilities or gain unauthorized access.


*   **Default Accounts and Passwords**

    * **Description**: Default accounts and their passwords are still enabled and unchanged.
    * **Example**: An admin account with the default password is still active.
    * **Impact**: Attackers can use the default credentials to gain administrative access.


*   **Overly Informative Error Handling**

    * **Description**: Error handling reveals stack traces or other overly informative error messages to users.
    * **Example**: An application displays a stack trace with sensitive information when an error occurs.
    * **Impact**: Attackers can use this information to identify vulnerabilities and attack vectors.


*   **Disabled or Insecurely Configured Security Features**

    * **Description**: Upgraded systems have the latest security features disabled or not configured securely.
    * **Example**: A web application does not enforce HTTPS even though the latest version supports it.
    * **Impact**: Data transmitted between the client and server can be intercepted and tampered with.


*   **Insecure Security Settings**

    * **Description**: Security settings in application servers, frameworks, libraries, databases, etc., are not set to secure values.
    * **Example**: A web server does not have secure cookie attributes set.
    * **Impact**: Attackers can exploit insecure cookies to hijack user sessions.


*   **Missing Security Headers**

    * **Description**: The server does not send security headers or directives, or they are not set to secure values.
    * **Example**: Missing Content Security Policy (CSP) headers.
    * **Impact**: The application is vulnerable to cross-site scripting (XSS) attacks.


* **Outdated or Vulnerable Software**
  * **Description**: The software is out of date or vulnerable.
  * **Example**: Using an outdated version of a library with known vulnerabilities.
  * **Impact**: Attackers can exploit these known vulnerabilities to compromise the applications

## Prevention Strategies

*   **Implement a Repeatable Hardening Process**

    * Ensure a fast, easy deployment of securely locked-down environments.
    * Configure development, QA, and production environments identically but with different credentials.
    * Automate the setup process to ensure consistency and reduce effort.


*   **Minimize the Platform**

    * Use a minimal platform by removing or not installing unused features, components, documentation, and samples.


*   **Regular Review and Update Configurations**

    * Regularly review and update configurations as part of the patch management process.
    * Address all security notes, updates, and patches.
    * Review permissions on cloud storage, such as S3 buckets.


*   **Segment Application Architecture**

    * Use segmentation, containerization, or cloud security groups to ensure secure separation between components or tenants.


*   **Send Security Directives to Clients**

    * Utilize security headers to enforce security policies on clients.


* **Automate Verification**
  * Implement an automated process to verify the effectiveness of configurations and settings across all environments.



***

## REFERENCES

* [OWASP Testing Guide: Configuration Management](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/02-Configuration\_and\_Deployment\_Management\_Testing/README)
* [OWASP Testing Guide: Testing for Error Codes](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/08-Testing\_for\_Error\_Handling/01-Testing\_For\_Improper\_Error\_Handling)
* [Application Security Verification Standard V14 Configuration](https://github.com/OWASP/ASVS/blob/master/4.0/en/0x22-V14-Config.md)
* [NIST Guide to General Server Hardening](https://csrc.nist.gov/publications/detail/sp/800-123/final)
* [CIS Security Configuration Guides/Benchmarks](https://www.cisecurity.org/cis-benchmarks/)
* [Amazon S3 Bucket Discovery and Enumeration](https://blog.websecurify.com/2017/10/aws-s3-bucket-discovery.html)
* [https://owasp.org/Top10/A05\_2021-Security\_Misconfiguration/](https://owasp.org/Top10/A05\_2021-Security\_Misconfiguration/)

## Mapped CWEs

*   **CWE-16: Configuration**

    * **Description**: Errors related to configuration settings.
    * **Link**: https://cwe.mitre.org/data/definitions/16.html


*   **CWE-23: Relative Path Traversal**

    * **Description**: The application allows attackers to access files outside the intended directory.
    * **Link**: https://cwe.mitre.org/data/definitions/23.html


*   **CWE-78: Improper Neutralization of Special Elements used in an OS Command ('OS Command Injection')**

    * **Description**: The application constructs OS commands using user input without proper neutralization of special characters.
    * **Link**: https://cwe.mitre.org/data/definitions/78.html


*   **CWE-89: SQL Injection**

    * **Description**: The application constructs SQL statements from user input, which attackers can manipulate to execute arbitrary SQL commands.
    * **Link**: https://cwe.mitre.org/data/definitions/89.html


*   **CWE-311: Missing Encryption of Sensitive Data**

    * **Description**: Sensitive data is not encrypted during storage or transmission.
    * **Link**: https://cwe.mitre.org/data/definitions/311.html


*   **CWE-538: File and Directory Information Exposure**

    * **Description**: The application exposes file and directory information.
    * **Link**: https://cwe.mitre.org/data/definitions/538.html


*   **CWE-548: Exposure of Information Through Directory Listing**

    * **Description**: The application allows directory listings, exposing files to attackers.
    * **Link**: https://cwe.mitre.org/data/definitions/548.html


*   **CWE-614: Sensitive Cookie in HTTPS Session Without 'Secure' Attribute**

    * **Description**: Cookies used in HTTPS sessions lack the 'Secure' attribute, making them vulnerable to interception.
    * **Link**: https://cwe.mitre.org/data/definitions/614.html


*   **CWE-611: Improper Restriction of XML External Entity Reference ('XXE')**

    * **Description**: The application processes XML input containing a reference to an external entity.
    * **Link**: https://cwe.mitre.org/data/definitions/611.html


* **CWE-798: Use of Hard-coded Credentials**
  * **Description**: The application contains hard-coded credentials for accessing the system.
  * **Link**: https://cwe.mitre.org/data/definitions/798.html
