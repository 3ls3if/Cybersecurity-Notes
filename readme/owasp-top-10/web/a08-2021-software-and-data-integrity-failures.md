# 8️⃣ A08:2021 – Software and Data Integrity Failures

## Software and Data Integrity Failures

Software and data integrity failures occur when code and infrastructure fail to protect against integrity violations. This vulnerability encompasses various scenarios, such as relying on untrusted sources for plugins, libraries, or modules, insecure CI/CD pipelines, and inadequate integrity verification during auto-update processes. Additionally, insecure deserialization, where objects or data are encoded in a vulnerable format, is another concern.

## Characteristics of Software and Data Integrity Failures

*   **Dependency on Untrusted Sources**

    * **Description**: Applications relying on plugins, libraries, or modules from untrusted repositories or CDNs.
    * **Example**: Integrating third-party libraries from unverified sources into the application.
    * **Impact**: Increases the risk of introducing malicious code or system compromise.


*   **Insecure CI/CD Pipelines**

    * **Description**: Vulnerabilities in the Continuous Integration/Continuous Deployment (CI/CD) pipeline allowing unauthorized access or code injection.
    * **Example**: Lack of proper access controls in the CI/CD process, enabling attackers to inject malicious code.
    * **Impact**: Compromises the integrity of the application and infrastructure.


*   **Inadequate Integrity Verification in Auto-updates**

    * **Description**: Auto-update mechanisms downloading and applying updates without sufficient integrity verification.
    * **Example**: Updates being distributed without cryptographic signatures or checksum verification.
    * **Impact**: Allows attackers to distribute and execute malicious updates on all installations.


* **Insecure Deserialization**
  * **Description**: Objects or data encoded or serialized in a vulnerable format susceptible to modification by attackers.
  * **Example**: Deserializing data without proper input validation and integrity checks.
  * **Impact**: Enables attackers to manipulate serialized objects and potentially execute arbitrary code.

## Prevention

*   **Use Digital Signatures**

    * Employ digital signatures or similar mechanisms to verify the software or data's authenticity and integrity.


*   **Trustworthy Dependency Management**

    * Ensure libraries and dependencies are sourced from trusted repositories, or consider hosting an internal vetted repository.


*   **Utilize Software Supply Chain Security Tools**

    * Employ tools like OWASP Dependency Check or OWASP CycloneDX to verify components for known vulnerabilities in the software supply chain.


*   **Implement Code and Configuration Review Processes**

    * Establish review processes for code and configuration changes to mitigate the risk of introducing malicious code or configuration into the software pipeline.


*   **Secure CI/CD Pipeline**

    * Configure the CI/CD pipeline with proper segregation, configuration, and access control to maintain the integrity of the code throughout the build and deploy processes.


* **Ensure Data Integrity for Untrusted Clients**
  * Prevent the transmission of unsigned or unencrypted serialized data to untrusted clients without integrity checks or digital signatures to detect tampering or replay attacks.



***

## References

* [OWASP Cheat Sheet: Infrastructure as Code](https://cheatsheetseries.owasp.org/cheatsheets/Infrastructure\_as\_Code\_Security\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Deserialization](https://www.owasp.org/index.php/Deserialization\_Cheat\_Sheet)
* [SAFECode Software Integrity Controls](https://safecode.org/publication/SAFECode\_Software\_Integrity\_Controls0610.pdf)
* [A 'Worst Nightmare' Cyberattack: The Untold Story Of The SolarWinds Hack](https://www.npr.org/2021/04/16/985439655/a-worst-nightmare-cyberattack-the-untold-story-of-the-solarwinds-hack)
* [CodeCov Bash Uploader Compromise](https://about.codecov.io/security-update)
* [Securing DevOps by Julien Vehent](https://www.manning.com/books/securing-devops)
* [https://owasp.org/Top10/A08\_2021-Software\_and\_Data\_Integrity\_Failures/](https://owasp.org/Top10/A08\_2021-Software\_and\_Data\_Integrity\_Failures/)

## Mapped CWEs

*   **CWE-829: Inclusion of Functionality from Untrusted Control Sphere**

    * CWE-829: Including functionality from untrusted sources increases the risk of code injection and system compromise.


*   **CWE-494: Download of Code Without Integrity Check**

    * CWE-494: Downloading code without integrity verification allows for the distribution and execution of malicious updates.


* **CWE-502: Deserialization of Untrusted Data**
  * CWE-502: Deserializing untrusted data without proper validation can lead to arbitrary code execution.
