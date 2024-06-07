# 🔟 A10:2021 – Server-Side Request Forgery (SSRF)

## Server-Side Request Forgery (SSRF)

Server-Side Request Forgery (SSRF) vulnerabilities occur when a web application fetches a remote resource without validating the user-supplied URL. This allows attackers to coerce the application into sending crafted requests to unintended destinations, potentially bypassing firewalls, VPNs, or other network access control mechanisms. With the increasing use of cloud services and complex architectures, the prevalence and severity of SSRF vulnerabilities have grown.

## Characteristics of Server-Side Request Forgery (SSRF)

*   **Fetching Remote Resources Without Validation**

    * **Description**: The application does not properly validate user-supplied URLs before fetching remote resources.
    * **Example**: A feature that fetches a website's metadata given a URL, without validating the URL format or domain.
    * **Impact**: Allows attackers to manipulate requests to internal services, potentially exposing sensitive information or internal endpoints.
    * **CWE-918: Server-Side Request Forgery (SSRF)**: https://cwe.mitre.org/data/definitions/918.html


*   **Bypassing Network Controls**

    * **Description**: SSRF can bypass network access controls like firewalls and VPNs by leveraging the server's access privileges.
    * **Example**: An attacker uses SSRF to access an internal admin panel that is otherwise protected by a firewall.
    * **Impact**: Can lead to unauthorized access to internal systems, data exfiltration, or further exploitation.
    * **CWE-918: Server-Side Request Forgery (SSRF)**: https://cwe.mitre.org/data/definitions/918.html


* **Impact on Cloud Services**
  * **Description**: Cloud services and complex architectures increase the attack surface and potential impact of SSRF vulnerabilities.
  * **Example**: Exploiting SSRF to access cloud metadata services and retrieve sensitive data such as access tokens.
  * **Impact**: Can lead to compromise of cloud infrastructure and services, potentially affecting multiple applications and users.
  * **CWE-918: Server-Side Request Forgery (SSRF)**: https://cwe.mitre.org/data/definitions/918.html

## Prevention

**Network Layer Controls:**

1. **Segment Remote Resource Access**:
   * Isolate remote resource access functionalities in separate networks.
2. **Deny by Default**:
   * Implement firewall policies that block all intranet traffic except for essential services.
3.  **Log Network Activity**:

    * Log all accepted and blocked network flows for monitoring and analysis.



**Application Layer Controls:**

1. **Sanitize and Validate Inputs**:
   * Sanitize and validate all user-supplied URLs.
2. **Enforce Allow List**:
   * Use a positive allow list for URL schema, port, and destination.
3. **Avoid Raw Responses**:
   * Do not send raw responses back to clients.
4. **Disable HTTP Redirections**:
   * Prevent HTTP redirections to avoid misuse.
5. **Ensure URL Consistency**:
   * Check URL consistency to prevent DNS rebinding and TOCTOU race conditions.
6.  **Avoid Deny Lists**:

    * Do not rely on deny lists or regular expressions for SSRF mitigation.



**Additional Measures:**

1. **Separate Security Services**:
   * Avoid deploying other security-relevant services on frontend systems.
2. **Control Local Traffic**:
   * Control local traffic on critical systems (e.g., localhost).
3. **Use Network Encryption**:
   * Implement network encryption (e.g., VPNs) for frontends with dedicated user groups requiring high security.

## Attack Scenarios

**Scenario #1: Port Scan Internal Servers**

* **Description**: If the network architecture lacks segmentation, attackers can perform internal network reconnaissance.
* **Example**: By sending SSRF payloads, attackers can determine open or closed ports on internal servers based on connection responses or elapsed time.
* **Impact**: This can reveal internal network structures and vulnerabilities, allowing attackers to plan further exploits.

**Scenario #2: Sensitive Data Exposure**

* **Description**: Attackers can access local files or internal services to obtain sensitive information.
* **Example**: Using SSRF, attackers might request resources such as `file:///etc/passwd` to read system files or `http://localhost:28017/` to access internal databases.
* **Impact**: This can lead to exposure of sensitive data, including system configuration files, user credentials, and internal service information.

**Scenario #3: Access Metadata Storage of Cloud Services**

* **Description**: Many cloud providers have metadata endpoints that can be accessed internally to retrieve configuration and credential information.
* **Example**: By exploiting SSRF, attackers can send requests to `http://169.254.169.254/` to obtain metadata from cloud services.
* **Impact**: This can result in exposure of sensitive cloud metadata, including access tokens and instance metadata, potentially compromising the entire cloud environment.

**Scenario #4: Compromise Internal Services**

* **Description**: Attackers can exploit SSRF to interact with internal services, potentially leading to more severe attacks.
* **Example**: By directing SSRF payloads to internal services, attackers could trigger Remote Code Execution (RCE) or cause Denial of Service (DoS).
* **Impact**: Successful exploitation could lead to full system compromise, service disruption, or further propagation of attacks within the internal network.



***

## References

* [OWASP - Server-Side Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server\_Side\_Request\_Forgery\_Prevention\_Cheat\_Sheet.html)
* [PortSwigger - Server-side request forgery (SSRF)](https://portswigger.net/web-security/ssrf)
* [Acunetix - What is Server-Side Request Forgery (SSRF)?](https://www.acunetix.com/blog/articles/server-side-request-forgery-vulnerability/)
* [SSRF bible](https://cheatsheetseries.owasp.org/assets/Server\_Side\_Request\_Forgery\_Prevention\_Cheat\_Sheet\_SSRF\_Bible.pdf)
* [A New Era of SSRF - Exploiting URL Parser in Trending Programming Languages!](https://www.blackhat.com/docs/us-17/thursday/us-17-Tsai-A-New-Era-Of-SSRF-Exploiting-URL-Parser-In-Trending-Programming-Languages.pdf)
* [https://owasp.org/Top10/A10\_2021-Server-Side\_Request\_Forgery\_%28SSRF%29/](https://owasp.org/Top10/A10\_2021-Server-Side\_Request\_Forgery\_\(SSRF\)/)

## Mapped CWEs

* **CWE-918: Server-Side Request Forgery (SSRF)**: https://cwe.mitre.org/data/definitions/918.html

