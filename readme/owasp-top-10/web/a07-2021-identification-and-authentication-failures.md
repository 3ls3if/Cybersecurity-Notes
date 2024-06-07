# 7️⃣ A07:2021 – Identification and Authentication Failures

## Identification and Authentication Failures

Properly managing user identity, authentication, and sessions is crucial for safeguarding against authentication-related attacks. Weaknesses in these areas can lead to unauthorized access and compromise sensitive data.

## Characteristics of Identification and Authentication Failures

*   **Permitting Automated Attacks**

    * **Description**: Allowing automated attacks like credential stuffing or brute force attacks.
    * **Example**: Lack of account lockout mechanism leading to repeated login attempts.
    * **Impact**: Increases the risk of unauthorized access by attackers using automated tools.


*   **Weak Passwords**

    * **Description**: Allowing default, weak, or well-known passwords, such as "Password1" or "admin/admin."
    * **Example**: Allowing users to set passwords without complexity requirements.
    * **Impact**: Increases the likelihood of successful brute force attacks or password guessing.


*   **Ineffective Credential Recovery**

    * **Description**: Using weak or ineffective processes for credential recovery and forgot-password functionalities.
    * **Example**: Relying solely on knowledge-based answers for password recovery.
    * **Impact**: Vulnerable to social engineering attacks or bypassing of authentication controls.


*   **Storage of Passwords**

    * **Description**: Storing passwords in plain text, encrypted, or using weak hashing algorithms.
    * **Example**: Storing passwords in a database without proper encryption or hashing.
    * **Impact**: Exposes passwords to potential theft or exploitation in case of a data breach.


*   **Missing or Ineffective Multi-factor Authentication (MFA)**

    * **Description**: Lack of or ineffective implementation of multi-factor authentication.
    * **Example**: Not requiring a second factor of authentication besides a password.
    * **Impact**: Decreases the resilience of authentication mechanisms against various attacks.


*   **Exposure of Session Identifier**

    * **Description**: Exposing session identifiers in URLs.
    * **Example**: Including session IDs as URL parameters.
    * **Impact**: Allows attackers to hijack sessions through session fixation or URL manipulation.


*   **Session Management Flaws**

    * **Description**: Reusing session identifiers after successful login or not properly invalidating session IDs.
    * **Example**: Allowing session IDs to remain active after logout or a period of inactivity.
    * **Impact**: Allows attackers to maintain unauthorized access even after the user attempts to log out.



## Prevention&#x20;

*   **Implement Multi-factor Authentication (MFA)**

    * Use MFA to mitigate automated credential stuffing, brute force, and stolen credential reuse attacks.


*   **Avoid Default Credentials**

    * Do not ship or deploy applications with default credentials, especially for admin users.


*   **Enforce Weak Password Checks**

    * Implement checks against commonly used weak passwords to improve password security.


*   **Adopt Strong Password Policies**

    * Align password policies with NIST 800-63b guidelines for Memorized Secrets to ensure appropriate length, complexity, and rotation.


*   **Harden Registration and Credential Recovery**

    * Ensure registration, credential recovery, and API pathways are hardened against account enumeration attacks by providing consistent messaging for all outcomes.


*   **Limit Failed Login Attempts**

    * Limit or gradually increase the delay for failed login attempts to prevent brute force attacks. Log all failures and alert administrators when attacks are detected.


* **Use Secure Session Management**
  * Employ a server-side, secure session manager that generates random session IDs with high entropy. Avoid session identifiers in URLs, securely store them, and invalidate sessions after logout, idle, and absolute timeouts.



***

## References

* [OWASP Proactive Controls: Implement Digital Identity](https://owasp.org/www-project-proactive-controls/v3/en/c6-digital-identity)
* [OWASP Application Security Verification Standard: V2 authentication](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Application Security Verification Standard: V3 Session Management](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Testing Guide: Identity](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/03-Identity\_Management\_Testing/README), [Authentication](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/04-Authentication\_Testing/README)
* [OWASP Cheat Sheet: Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Credential Stuffing](https://cheatsheetseries.owasp.org/cheatsheets/Credential\_Stuffing\_Prevention\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot\_Password\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session\_Management\_Cheat\_Sheet.html)
* [OWASP Automated Threats Handbook](https://owasp.org/www-project-automated-threats-to-web-applications/)
* [NIST 800-63b: 5.1.1 Memorized Secrets](https://pages.nist.gov/800-63-3/sp800-63b.html#memsecret)
* [https://owasp.org/Top10/A07\_2021-Identification\_and\_Authentication\_Failures/](https://owasp.org/Top10/A07\_2021-Identification\_and\_Authentication\_Failures/)

## Mapped CWEs

*   **Implement Multi-factor Authentication (MFA)**

    * CWE-306: https://cwe.mitre.org/data/definitions/306.html


*   **Avoid Default Credentials**

    * CWE-798: https://cwe.mitre.org/data/definitions/798.html


*   **Enforce Weak Password Checks**

    * CWE-521: https://cwe.mitre.org/data/definitions/521.html


*   **Adopt Strong Password Policies**

    * CWE-263: https://cwe.mitre.org/data/definitions/263.html


*   **Harden Registration and Credential Recovery**

    * CWE-254: https://cwe.mitre.org/data/definitions/254.html


*   **Limit Failed Login Attempts**

    * CWE-489: https://cwe.mitre.org/data/definitions/489.html


*   **Use Secure Session Management**

    * CWE-384: https://cwe.mitre.org/data/definitions/384.html


* **Use Secure Session Management**
  * CWE-770: https://cwe.mitre.org/data/definitions/770.html\
