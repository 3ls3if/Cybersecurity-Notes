# 1️⃣ A01:2021 – Broken Access Control

## What is Broken Access Control?

Broken access control vulnerabilities occur when applications do not correctly enforce policies that restrict users' actions to those intended by the system’s administrators. These vulnerabilities can lead to unauthorized information disclosure, modification, or destruction of data, or performing unauthorized business functions.

Here are some common types of broken access control vulnerabilities:

1. **Violation of the Principle of Least Privilege or Deny by Default**
   * **Description**: Access should be granted only to specific users, roles, or capabilities, but instead, it is available to anyone. This often happens when the system does not properly restrict access to resources, leading to users gaining more permissions than necessary.
   * **Impact**: Users can access or modify data and functionalities that they should not be allowed to, leading to potential data breaches and system compromise.
2. **Bypassing Access Control Checks**
   * **Description**: Users can manipulate application inputs such as URLs, parameters, or internal states to bypass access control mechanisms. This includes parameter tampering, force browsing, and modifying HTML pages or API requests.
   * **Impact**: Unauthorized users can gain access to restricted areas or data, compromising the integrity and confidentiality of the system.
3. **Insecure Direct Object References (IDOR)**
   * **Description**: Users can access resources by modifying the unique identifiers used by the application, such as changing a user ID in a URL. The application does not verify if the user is authorized to access the specified resource.
   * **Impact**: Users can access or modify data that belongs to other users, leading to data leakage and potential data corruption.
4. **Missing Access Controls for API Methods**
   * **Description**: APIs lack proper access controls for critical operations such as POST, PUT, DELETE, leading to unauthorized users performing these actions.
   * **Impact**: Unauthorized users can create, update, or delete resources, causing data integrity issues and potential system disruption.
5. **Elevation of Privilege**
   * **Description**: Users can elevate their privileges without proper authorization, such as accessing admin functionalities while logged in as a standard user, or acting as a user without being logged in.
   * **Impact**: Attackers can gain administrative control, manipulate critical data, and potentially compromise the entire system.
6. **Metadata Manipulation**
   * **Description**: Manipulating metadata such as JSON Web Tokens (JWT), cookies, or hidden fields to elevate privileges or bypass access controls. This includes replaying or tampering with tokens.
   * **Impact**: Attackers can gain unauthorized access or elevated privileges, leading to data breaches and unauthorized actions within the application.
7. **CORS Misconfiguration**
   * **Description**: Cross-Origin Resource Sharing (CORS) settings allow unauthorized or untrusted origins to access the API. This misconfiguration can expose sensitive endpoints to malicious websites.
   * **Impact**: Attackers can exploit the API from untrusted origins, leading to unauthorized actions and data leakage.
8. **Force Browsing**
   * **Description**: Users can access authenticated or privileged pages without proper authentication or authorization by directly navigating to these pages.
   * **Impact**: Unauthorized users can access restricted functionalities and data, compromising the security and integrity of the application.

## Mitigation Strategies

To prevent broken access control vulnerabilities, implement the following strategies:

* Enforce the principle of least privilege.
* Implement comprehensive access control checks on both client and server sides.
* Use secure coding practices to prevent IDOR.
* Ensure proper access controls for all API methods.
* Validate and securely handle JWT tokens.
* Configure CORS correctly to restrict access to trusted origins.
* Implement proper authentication and session management mechanisms.



***

## Practical Scenario

#### Scenario: Online Banking Application

**1. Violation of the Principle of Least Privilege**

* **Description**: A user should only have access to their own account details and not those of others. However, the application grants access to all users' accounts to any logged-in user.
* **Example**:
  * **Intended Functionality**: User Alice should only access `https://bankapp.com/account/alice`.
  * **Broken Functionality**: User Alice can also access `https://bankapp.com/account/bob`.

```javascript
javascriptCopy code// Code example where privilege is not enforced properly
app.get('/account/:username', (req, res) => {
    // The server doesn't check if the logged-in user is the owner of the account
    const username = req.params.username;
    const accountData = getAccountData(username);
    res.send(accountData);
});
```

**2. Bypassing Access Control Checks**

* **Description**: A user can bypass access control by manipulating the URL.
* **Example**:
  * **Intended Functionality**: Only the account owner can view their transactions.
  * **Broken Functionality**: Any user can view another user's transactions by changing the URL.

```javascript
javascriptCopy code// Intended URL for viewing transactions
https://bankapp.com/transactions?user=alice

// Attacker changes the URL to view someone else's transactions
https://bankapp.com/transactions?user=bob
```

**3. Insecure Direct Object References (IDOR)**

* **Description**: Users can access resources by manipulating the unique identifier.
* **Example**:
  * **Intended Functionality**: User Alice can view and edit only her profile.
  * **Broken Functionality**: User Alice can access Bob's profile by changing the user ID in the request.

```javascript
javascriptCopy code// URL for accessing user profile
https://bankapp.com/profile?user_id=123

// Attacker changes user_id to access another user's profile
https://bankapp.com/profile?user_id=456
```

**4. Missing Access Controls for API Methods**

* **Description**: APIs lack proper access controls for critical operations like POST, PUT, DELETE.
* **Example**:
  * **Intended Functionality**: Only the owner can delete their account.
  * **Broken Functionality**: Any user can delete any account.

```javascript
javascriptCopy code// Missing access control on API endpoint
app.delete('/api/deleteAccount', (req, res) => {
    const userId = req.body.userId;
    deleteUserAccount(userId);
    res.send('Account deleted');
});

// Attacker sends a delete request for another user
fetch('https://bankapp.com/api/deleteAccount', {
    method: 'DELETE',
    body: JSON.stringify({ userId: '456' })
});
```

**5. Elevation of Privilege**

* **Description**: A user can elevate their privileges without proper authorization.
* **Example**:
  * **Intended Functionality**: Standard users cannot access admin functionalities.
  * **Broken Functionality**: A standard user can elevate their privileges to admin.

```javascript
javascriptCopy code// URL for admin panel
https://bankapp.com/admin

// Attacker discovers the URL and accesses it without admin credentials
```

**6. Metadata Manipulation (JWT Tampering)**

* **Description**: Manipulating the JWT token to elevate privileges.
* **Example**:
  * **Intended Functionality**: Users cannot modify their JWT tokens.
  * **Broken Functionality**: Users can tamper with their tokens to gain admin access.

```javascript
javascriptCopy code// Original JWT payload
{
    "user": "alice",
    "role": "user"
}

// Attacker modifies the JWT payload
{
    "user": "alice",
    "role": "admin"
}
```

**7. CORS Misconfiguration**

* **Description**: API accessible from unauthorized/untrusted origins due to improper CORS settings.
* **Example**:
  * **Intended Functionality**: Only requests from `https://trustedapp.com` are allowed.
  * **Broken Functionality**: Requests from any origin are allowed.

```javascript
javascriptCopy code// Incorrect CORS configuration
app.use(cors({
    origin: '*'
}));

// This should be
app.use(cors({
    origin: 'https://trustedapp.com'
}));
```

**8. Force Browsing**

* **Description**: Accessing pages meant for authenticated users as an unauthenticated user or accessing privileged pages as a standard user.
* **Example**:
  * **Intended Functionality**: Only authenticated users can access their dashboard.
  * **Broken Functionality**: Unauthenticated users can access the dashboard.

```javascript
javascriptCopy code// URL for user dashboard
https://bankapp.com/dashboard

// Attacker tries to access the dashboard without logging in
```



***

## REFERENCES

* [https://owasp.org/Top10/A01\_2021-Broken\_Access\_Control/](https://owasp.org/Top10/A01\_2021-Broken\_Access\_Control/)
* [OWASP Proactive Controls: Enforce Access Controls](https://owasp.org/www-project-proactive-controls/v3/en/c7-enforce-access-controls)
* [OWASP Application Security Verification Standard: V4 Access Control](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Testing Guide: Authorization Testing](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/05-Authorization\_Testing/README)
* [OWASP Cheat Sheet: Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization\_Cheat\_Sheet.html)
* [PortSwigger: Exploiting CORS misconfiguration](https://portswigger.net/blog/exploiting-cors-misconfigurations-for-bitcoins-and-bounties)
* [OAuth: Revoking Access](https://www.oauth.com/oauth2-servers/listing-authorizations/revoking-access/)

## Mapped CWEs

1. **Violation of the Principle of Least Privilege or Deny by Default**
   * **CWE-284**: [Improper Access Control](https://cwe.mitre.org/data/definitions/284.html)
2. **Bypassing Access Control Checks**
   * **CWE-22**: [Path Traversal](https://cwe.mitre.org/data/definitions/22.html)
   * **CWE-425**: [Direct Request ('Forced Browsing')](https://cwe.mitre.org/data/definitions/425.html)
3. **Insecure Direct Object References (IDOR)**
   * **CWE-639**: [Authorization Bypass Through User-Controlled Key](https://cwe.mitre.org/data/definitions/639.html)
4. **Missing Access Controls for API Methods**
   * **CWE-284**: [Improper Access Control](https://cwe.mitre.org/data/definitions/284.html)
5. **Elevation of Privilege**
   * **CWE-269**: [Improper Privilege Management](https://cwe.mitre.org/data/definitions/269.html)
   * **CWE-250**: [Execution with Unnecessary Privileges](https://cwe.mitre.org/data/definitions/250.html)
6. **Metadata Manipulation (JWT Tampering)**
   * **CWE-347**: [Improper Verification of Cryptographic Signature](https://cwe.mitre.org/data/definitions/347.html)
   * **CWE-565**: [Reliance on Cookies without Validation and Integrity Checking](https://cwe.mitre.org/data/definitions/565.html)
7. **CORS Misconfiguration**
   * **CWE-942**: [Permissive Cross-domain Policy with Untrusted Domains](https://cwe.mitre.org/data/definitions/942.html)
8. **Force Browsing**
   * **CWE-425**: [Direct Request ('Forced Browsing')](https://cwe.mitre.org/data/definitions/425.html)

