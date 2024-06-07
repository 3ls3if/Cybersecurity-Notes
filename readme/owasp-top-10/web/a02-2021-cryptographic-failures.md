# 2️⃣ A02:2021 – Cryptographic Failures

## Cryptographic Failures

Cryptographic failures occur when data protection mechanisms fail to adequately secure data in transit or at rest, resulting in potential unauthorized access, data breaches, or other security issues. These failures can be caused by various factors, including the use of outdated or weak algorithms, improper key management, and misconfigured encryption protocols.

Here are some detailed descriptions and examples of common cryptographic failures:

1. **Transmission of Data in Clear Text**
   * **Description**: Data is transmitted over insecure protocols such as HTTP, SMTP, or FTP without encryption.
   * **Example**: An e-commerce website transmits login credentials over HTTP instead of HTTPS, allowing an attacker to intercept the credentials using a network sniffer.
   * **Impact**: Exposure of sensitive data to interception by unauthorized parties.
   * **CWE**: CWE-319
2. **Use of Old or Weak Cryptographic Algorithms or Protocols**
   * **Description**: Outdated algorithms or protocols like SSL 2.0/3.0, RC4, or DES are used, which have known vulnerabilities.
   * **Example**: A legacy system uses DES encryption to protect stored credit card information. An attacker exploits the weak encryption to decrypt the credit card data.
   * **Impact**: Increased risk of data being decrypted or tampered with by attackers.
   * **CWE**: CWE-327
3. **Improper Key Management**
   * **Description**: Use of default, weak, or reused cryptographic keys, improper key rotation, or keys checked into source code repositories.
   * **Example**: A developer checks in the cryptographic keys into a public GitHub repository, exposing them to anyone who accesses the repository.
   * **Impact**: Compromised encryption keys can lead to unauthorized data access.
   * **CWE**: CWE-320
4. **Encryption Not Enforced**
   * **Description**: Missing HTTP security headers or directives that enforce encryption.
   * **Example**: A web application does not implement HTTP Strict Transport Security (HSTS), allowing an attacker to downgrade the connection from HTTPS to HTTP.
   * **Impact**: Browsers and other clients may communicate over unencrypted connections, exposing sensitive data.
   * **CWE**: CWE-523
5. **Improper Certificate Validation**
   * **Description**: Failure to properly validate server certificates and trust chains.
   * **Example**: A mobile app does not validate the server's SSL certificate, making it vulnerable to man-in-the-middle (MITM) attacks.
   * **Impact**: Increased risk of MITM attacks.
   * **CWE**: CWE-295
6. **Insecure Cryptographic Modes and Initialization Vectors**
   * **Description**: Ignoring, reusing, or improperly generating initialization vectors (IVs) for encryption, or using insecure modes like ECB.
   * **Example**: An application uses ECB mode for AES encryption, which can reveal patterns in the plaintext data.
   * **Impact**: Weak encryption that can be easily broken by attackers.
   * **CWE**: CWE-329, CWE-780
7. **Inappropriate Use of Passwords as Cryptographic Keys**
   * **Description**: Using passwords directly as cryptographic keys without a key derivation function.
   * **Example**: An application uses a user's password directly as the key for AES encryption, making it vulnerable to brute-force attacks.
   * **Impact**: Vulnerability to brute-force attacks and weaker security.
   * **CWE**: CWE-261
8. **Insufficient Randomness for Cryptographic Purposes**
   * **Description**: Using random number generators that do not meet cryptographic standards, or improperly seeding them.
   * **Example**: A developer uses `rand()` for generating encryption keys instead of a cryptographically secure random number generator.
   * **Impact**: Predictable cryptographic operations that can be exploited by attackers.
   * **CWE**: CWE-332
9. **Use of Deprecated Hash Functions**
   * **Description**: Utilizing hash functions like MD5 or SHA1, which are no longer considered secure.
   * **Example**: An application uses MD5 to hash user passwords, making it vulnerable to collision attacks.
   * **Impact**: Increased risk of hash collisions and successful attack attempts.
   * **CWE**: CWE-328
10. **Use of Deprecated Cryptographic Padding Methods**
    * **Description**: Employing outdated padding schemes such as PKCS #1 v1.5.
    * **Example**: An application uses PKCS #1 v1.5 padding for RSA encryption, which is susceptible to padding oracle attacks.
    * **Impact**: Vulnerability to padding oracle attacks and other cryptographic exploits.
    * **CWE**: CWE-324
11. **Exploitable Cryptographic Error Messages or Side Channel Information**
    * **Description**: Error messages or side-channel information that reveal details about the cryptographic process, such as in padding oracle attacks.
    * **Example**: A web application returns different error messages for padding errors versus decryption errors, allowing an attacker to perform a padding oracle attack.
    * **Impact**: Attackers can exploit these leaks to decrypt data or compromise the encryption process.
    * **CWE**: CWE-209, CWE-203

## Mitigation Strategies

* **Encrypt Data in Transit and at Rest**: Use strong encryption protocols (e.g., TLS 1.2 or higher) for data transmission and encrypt sensitive data stored on disk.
* **Use Strong Cryptographic Algorithms**: Implement secure algorithms like AES for encryption, and SHA-256 or SHA-3 for hashing.
* **Implement Proper Key Management**: Use secure key generation, storage, rotation, and avoid hardcoding keys in source code.
* **Enforce Encryption Through Security Headers**: Use HTTP security headers like Strict-Transport-Security (HSTS) to enforce HTTPS.
* **Validate Certificates Properly**: Ensure certificates and their trust chains are correctly validated to prevent MITM attacks.
* **Use Secure Modes and IVs**: Implement secure modes of operation (e.g., GCM, CBC with HMAC) and properly generate and manage IVs.
* **Derive Keys Securely**: Use password-based key derivation functions (e.g., PBKDF2, bcrypt, scrypt) instead of passwords directly as keys.
* **Ensure Sufficient Randomness**: Use cryptographically secure random number generators and ensure they are properly seeded.
* **Avoid Deprecated Hash Functions**: Use current, secure hash functions like SHA-256 or SHA-3.
* **Avoid Deprecated Padding Methods**: Implement modern padding schemes and avoid deprecated methods.
* **Handle Cryptographic Errors Securely**: Ensure cryptographic processes do not leak information through error messages or side channels.

***

## REFERENCES

* [OWASP Proactive Controls: Protect Data Everywhere](https://owasp.org/www-project-proactive-controls/v3/en/c8-protect-data-everywhere)
* [OWASP Application Security Verification Standard (V7, 9, 10)](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Cheat Sheet: Transport Layer Protection](https://cheatsheetseries.owasp.org/cheatsheets/Transport\_Layer\_Protection\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: User Privacy Protection](https://cheatsheetseries.owasp.org/cheatsheets/User\_Privacy\_Protection\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password\_Storage\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Cryptographic Storage](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic\_Storage\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: HSTS](https://cheatsheetseries.owasp.org/cheatsheets/HTTP\_Strict\_Transport\_Security\_Cheat\_Sheet.html)
* [OWASP Testing Guide: Testing for weak cryptography](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web\_Application\_Security\_Testing/09-Testing\_for\_Weak\_Cryptography/README)
* [https://owasp.org/Top10/A02\_2021-Cryptographic\_Failures/](https://owasp.org/Top10/A02\_2021-Cryptographic\_Failures/)

## Mapped CWEs

* **Transmission of Data in Clear Text**
  * **CWE-319**: [Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html)
* **Use of Old or Weak Cryptographic Algorithms or Protocols**
  * **CWE-327**: [Use of a Broken or Risky Cryptographic Algorithm](https://cwe.mitre.org/data/definitions/327.html)
* **Improper Key Management**
  * **CWE-320**: [Key Management Errors](https://cwe.mitre.org/data/definitions/320.html)
* **Encryption Not Enforced**
  * **CWE-523**: [Unprotected Transport of Credentials](https://cwe.mitre.org/data/definitions/523.html)
* **Improper Certificate Validation**
  * **CWE-295**: [Improper Certificate Validation](https://cwe.mitre.org/data/definitions/295.html)
* **Insecure Cryptographic Modes and Initialization Vectors**
  * **CWE-329**: [Not Using a Random IV with CBC Mode](https://cwe.mitre.org/data/definitions/329.html)
  * **CWE-780**: [Use of Improper Cryptographic Primitive](https://cwe.mitre.org/data/definitions/780.html)
* **Inappropriate Use of Passwords as Cryptographic Keys**
  * **CWE-261**: [Weak Cryptography for Passwords](https://cwe.mitre.org/data/definitions/261.html)
* **Insufficient Randomness for Cryptographic Purposes**
  * **CWE-332**: [Insufficient Entropy](https://cwe.mitre.org/data/definitions/332.html)
* **Use of Deprecated Hash Functions**
  * **CWE-328**: [Use of a Weak Hash Function](https://cwe.mitre.org/data/definitions/328.html)
* **Use of Deprecated Cryptographic Padding Methods**
  * **CWE-324**: [Use of a Key Past its Expiration Date](https://cwe.mitre.org/data/definitions/324.html)
* **Exploitable Cryptographic Error Messages or Side Channel Information**
  * **CWE-209**: [Information Exposure Through an Error Message](https://cwe.mitre.org/data/definitions/209.html)
  * **CWE-203**: [Information Exposure Through Discrepancy](https://cwe.mitre.org/data/definitions/203.html)
