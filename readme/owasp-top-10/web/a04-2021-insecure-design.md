# 4️⃣ A04:2021 – Insecure Design

## Insecure Design

Insecure design refers to weaknesses arising from the absence or ineffectiveness of security controls in the system's architecture. Unlike implementation flaws, which are errors in coding or configuration, insecure design represents fundamental issues in the system's conceptualization. These weaknesses result from a failure to integrate adequate security measures during the design phase, which cannot be rectified merely through flawless implementation.

## Characteristics of Insecure Design Vulnerabilities

*   **Missing or Ineffective Control Design**

    * **Description**: Security controls are either absent or insufficiently designed to address potential threats and risks.
    * **Example**: An application does not include multi-factor authentication (MFA) for sensitive transactions.
    * **Impact**: Without MFA, attackers can easily compromise accounts using stolen credentials.


*   **Lack of Business Risk Profiling**

    * **Description**: Failure to assess and incorporate the business risk profile into the software or system design.
    * **Example**: A financial application does not assess the impact of potential fraud and, therefore, lacks adequate anti-fraud mechanisms.
    * **Impact**: The application is more susceptible to fraudulent activities, leading to significant financial losses.


*   **Failure to Determine Required Security Levels**

    * **Description**: Inadequate determination of the necessary security controls based on the data sensitivity and the operational environment.
    * **Example**: A healthcare system does not encrypt sensitive patient records stored in its database.
    * **Impact**: Unauthorized access to the database can lead to significant breaches of patient confidentiality and legal repercussions.


*   **No Threat Modeling**

    * **Description**: Absence of a systematic process to identify, enumerate, and prioritize potential threats.
    * **Example**: A web application does not undergo threat modeling to identify and mitigate possible attack vectors.
    * **Impact**: Potential security weaknesses remain unaddressed, increasing the risk of successful attacks.


*   **Inadequate Security Requirements Specification**

    * **Description**: Insufficient specification of security requirements during the system's design phase.
    * **Example**: An e-commerce platform does not specify secure payment processing requirements.
    * **Impact**: The platform might implement insecure payment methods, leading to data breaches and financial fraud.


* **Ignoring Security by Design Principles**
  * **Description**: Failure to integrate security principles, such as least privilege and defense in depth, into the system's design.
  * **Example**: A social media application allows users to upload files without restrictions or checks.
  * **Impact**: Attackers can upload malicious files, compromising the application's security.

## Common Insecure Design Vulnerabilities

*   **Lack of Input Validation**

    * **Description**: The application design does not account for proper input validation, leading to various injection attacks.
    * **Example**: A login form does not validate user input, making it vulnerable to SQL injection.
    * **Impact**: Attackers can manipulate database queries, accessing or modifying unauthorized data.


*   **Improper Session Management**

    * **Description**: Inadequate design of session management mechanisms, such as secure session identifiers and timeouts.
    * **Example**: Sessions do not expire after prolonged inactivity.
    * **Impact**: Attackers can hijack inactive sessions, gaining unauthorized access to user accounts.


*   **Unsecured Data Storage**

    * **Description**: The system does not design for secure storage of sensitive data, such as passwords or personal information.
    * **Example**: Passwords are stored in plaintext in the database.
    * **Impact**: If the database is compromised, attackers can directly access users' passwords.


*   **Inadequate Error Handling**

    * **Description**: The system design does not incorporate proper error handling and logging mechanisms.
    * **Example**: Detailed error messages are displayed to users.
    * **Impact**: Attackers can gain insights into the system's structure and potential vulnerabilities.


* **Insufficient Access Controls**
  * **Description**: Lack of adequate access control mechanisms in the system design.
  * **Example**: An administrative interface is accessible without proper authentication.
  * **Impact**: Unauthorized users can access and manipulate administrative functions.

## Mitigation Strategies

* Establish and use a secure development lifecycle with AppSec professionals to help evaluate and design security and privacy-related controls
* Establish and use a library of secure design patterns or paved road ready to use components
* Use threat modeling for critical authentication, access control, business logic, and key flows
* Integrate security language and controls into user stories
* Integrate plausibility checks at each tier of your application (from frontend to backend)
* Write unit and integration tests to validate that all critical flows are resistant to the threat model. Compile use-cases _and_ misuse-cases for each tier of your application.
* Segregate tier layers on the system and network layers depending on the exposure and protection needs
* Segregate tenants robustly by design throughout all tiers
* Limit resource consumption by user or service



***

## REFERENCES

* [OWASP Cheat Sheet: Secure Design Principles](https://cheatsheetseries.owasp.org/cheatsheets/Secure\_Product\_Design\_Cheat\_Sheet.html)
* [OWASP SAMM: Design:Security Architecture](https://owaspsamm.org/model/design/security-architecture/)
* [OWASP SAMM: Design:Threat Assessment](https://owaspsamm.org/model/design/threat-assessment/)
* [NIST – Guidelines on Minimum Standards for Developer Verification of Software](https://www.nist.gov/publications/guidelines-minimum-standards-developer-verification-software)
* [The Threat Modeling Manifesto](https://threatmodelingmanifesto.org/)
* [Awesome Threat Modeling](https://github.com/hysnsec/awesome-threat-modelling)
* [https://owasp.org/Top10/A04\_2021-Insecure\_Design/](https://owasp.org/Top10/A04\_2021-Insecure\_Design/)

## Mapped CWEs

*   **CWE-276: Incorrect Default Permissions**

    * **Description**: The application sets incorrect default permissions, leading to excessive access.
    * **Link**: https://cwe.mitre.org/data/definitions/276.html


*   **CWE-602: Client-Side Enforcement of Server-Side Security**

    * **Description**: Security decisions are made on the client side rather than on the server side.
    * **Link**: https://cwe.mitre.org/data/definitions/602.html


*   **CWE-209: Generation of Error Message Containing Sensitive Information**

    * **Description**: The application generates error messages that include sensitive information.
    * **Link**: https://cwe.mitre.org/data/definitions/209.html


*   **CWE-311: Missing Encryption of Sensitive Data**

    * **Description**: Sensitive data is not encrypted during storage or transmission.
    * **Link**: https://cwe.mitre.org/data/definitions/311.html


*   **CWE-327: Use of a Broken or Risky Cryptographic Algorithm**

    * **Description**: The application uses cryptographic algorithms that are considered broken or risky.
    * **Link**: https://cwe.mitre.org/data/definitions/327.html


*   **CWE-693: Protection Mechanism Failure**

    * **Description**: A protection mechanism, such as authentication or access control, fails to perform correctly.
    * **Link**: https://cwe.mitre.org/data/definitions/693.html


*   **CWE-613: Insufficient Session Expiration**

    * **Description**: The application fails to properly expire sessions after a period of inactivity or a predefined time limit.
    * **Link**: https://cwe.mitre.org/data/definitions/613.html


*   **CWE-798: Use of Hard-coded Credentials**

    * **Description**: The application contains hard-coded credentials for accessing the system.
    * **Link**: https://cwe.mitre.org/data/definitions/798.html


*   **CWE-770: Allocation of Resources Without Limits or Throttling**

    * **Description**: The application does not enforce limits or throttling on resource allocation.
    * **Link**: https://cwe.mitre.org/data/definitions/770.html


*   **CWE-306: Missing Authentication for Critical Function**

    * **Description**: The application fails to require authentication for accessing critical functions.
    * **Link**: https://cwe.mitre.org/data/definitions/306.html


*   **CWE-269: Improper Privilege Management**

    * **Description**: The application improperly manages user privileges.
    * **Link**: https://cwe.mitre.org/data/definitions/269.html


* **CWE-501: Trust Boundary Violation**
  * **Description**: The application fails to enforce trust boundaries correctly.
  * **Link**: https://cwe.mitre.org/data/definitions/501.html
