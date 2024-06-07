# 3️⃣ A03:2021 – Injection

## Injection

Injection vulnerabilities occur when an application processes untrusted data and executes unintended commands or queries. This typically happens when user-supplied data is not properly validated, filtered, or sanitized, allowing attackers to manipulate the interpreter's execution context.

Here are detailed descriptions and examples of injection vulnerabilities:

**When an Application is Vulnerable to Injection?**

1.  **User-Supplied Data is Not Validated, Filtered, or Sanitized**

    * **Description**: The application accepts input from users without validating, filtering, or sanitizing it, leading to potential security risks.
    * **Example**: A web form allows users to enter their username without any input validation or sanitization.
    * **Impact**: Attackers can input malicious scripts or SQL commands that the application executes, leading to data breaches or system compromise.


2.  **Dynamic Queries or Non-Parameterized Calls Without Context-Aware Escaping**

    * **Description**: The application constructs queries or commands using dynamic strings that include user input without proper context-aware escaping.
    *   **Example**: Constructing an SQL query by concatenating strings, such as:

        ```sql
        String query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'";
        ```
    * **Impact**: Attackers can inject SQL commands that alter the query's behavior, potentially accessing unauthorized data.


3.  **Hostile Data Used in Object-Relational Mapping (ORM) Search Parameters**

    * **Description**: The application uses user-supplied data in ORM search parameters without proper validation, allowing attackers to extract sensitive records.
    *   **Example**: Using unvalidated user input in an ORM query:

        ```java
        List<User> users = entityManager.createQuery("SELECT u FROM User u WHERE u.name = '" + name + "'").getResultList();
        ```
    * **Impact**: Attackers can manipulate ORM queries to extract additional records or sensitive data.


4. **Hostile Data Directly Used or Concatenated in Dynamic Queries, Commands, or Stored Procedures**
   * **Description**: User input is directly included in dynamic queries, commands, or stored procedures without validation or sanitization.
   *   **Example**: Directly using user input in a shell command:

       ```python
       os.system("echo " + user_input)
       ```
   * **Impact**: Attackers can inject malicious commands that the system executes, potentially leading to arbitrary command execution.

## Common Types of Injection

1.  **SQL Injection**

    * **Description**: Manipulating SQL queries by injecting malicious input.
    * **Example**: Injecting `' OR '1'='1` into a login form to bypass authentication.


2.  **NoSQL Injection**

    * **Description**: Manipulating NoSQL queries with malicious input.
    * **Example**: Injecting `{"$ne": null}` in a MongoDB query to bypass authentication.


3.  **OS Command Injection**

    * **Description**: Executing arbitrary operating system commands via injected input.
    * **Example**: Injecting `; rm -rf /` into a command execution function.


4.  **ORM Injection**

    * **Description**: Manipulating ORM queries with malicious input.
    * **Example**: Injecting `1=1` in an ORM search parameter to retrieve all records.


5.  **LDAP Injection**

    * **Description**: Manipulating LDAP queries with malicious input.
    * **Example**: Injecting `*` in an LDAP search filter to retrieve all entries.


6. **Expression Language (EL) or Object Graph Navigation Library (OGNL) Injection**
   * **Description**: Injecting malicious data into EL or OGNL expressions.
   * **Example**: Injecting `${"".getClass().forName("java.lang.Runtime").getRuntime().exec("calc")}` to execute a command.

## Detection and Prevention

* **Source Code Review**: Manual review of source code to identify potential injection points.
* **Automated Testing**: Using automated tools to test all parameters, headers, URLs, cookies, JSON, SOAP, and XML inputs for injection vulnerabilities.
* **Static Application Security Testing (SAST)**: Analyzes source code for vulnerabilities without executing the application.
* **Dynamic Application Security Testing (DAST)**: Tests the application in runtime to identify vulnerabilities by simulating attacks.
* **Interactive Application Security Testing (IAST)**: Combines SAST and DAST techniques to analyze running applications.

## Mitigation Strategies

*   **Input Validation and Sanitization**

    * **Description**: Validate and sanitize all user inputs to ensure they conform to expected formats and contain no malicious content.
    * **Example**: Use a whitelist of allowed characters for input fields.


*   **Parameterized Queries and Prepared Statements**

    * **Description**: Use parameterized queries and prepared statements to separate data from code.
    *   **Example**: Use `PreparedStatement` in Java to execute SQL queries:

        ```java
        String query = "SELECT * FROM users WHERE username = ? AND password = ?";
        PreparedStatement stmt = connection.prepareStatement(query);
        stmt.setString(1, username);
        stmt.setString(2, password);
        ResultSet rs = stmt.executeQuery();
        ```




*   **Context-Aware Escaping**

    * **Description**: Apply escaping based on the context in which the data is used (e.g., SQL, HTML, XML).
    * **Example**: Use appropriate escaping libraries to sanitize user input before using it in different contexts.


*   **Least Privilege Principle**

    * **Description**: Limit the privileges of application accounts and use read-only database accounts where possible.
    * **Example**: Configure the application to connect to the database with a user account that has minimal privileges necessary for its operation.


* **Security Testing**
  * **Description**: Incorporate regular security testing into the development lifecycle using SAST, DAST, and IAST tools.
  * **Example**: Integrate a DAST tool into the CI/CD pipeline to automatically scan for injection vulnerabilities during the build process.



***

## REFERENCES

* [OWASP Proactive Controls: Secure Database Access](https://owasp.org/www-project-proactive-controls/v3/en/c3-secure-database)
* [OWASP ASVS: V5 Input Validation and Encoding](https://owasp.org/www-project-application-security-verification-standard)
* [OWASP Testing Guide: SQL Injection,](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/05-Testing\_for\_SQL\_Injection) [Command Injection](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/12-Testing\_for\_Command\_Injection), and [ORM Injection](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/05.7-Testing\_for\_ORM\_Injection)
* [OWASP Cheat Sheet: Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL\_Injection\_Prevention\_Cheat\_Sheet.html)
* [OWASP Cheat Sheet: Injection Prevention in Java](https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet\_in\_Java.html)
* [OWASP Cheat Sheet: Query Parameterization](https://cheatsheetseries.owasp.org/cheatsheets/Query\_Parameterization\_Cheat\_Sheet.html)
* [OWASP Automated Threats to Web Applications – OAT-014](https://owasp.org/www-project-automated-threats-to-web-applications/)
* [PortSwigger: Server-side template injection](https://portswigger.net/kb/issues/00101080\_serversidetemplateinjection)
* [https://owasp.org/Top10/A03\_2021-Injection/](https://owasp.org/Top10/A03\_2021-Injection/)

## Mapped CWEs

*   **CWE-20: Improper Input Validation**

    * **Description**: The application does not validate or improperly validates input that can affect the control flow or data flow of a program.
    * **Link**: https://cwe.mitre.org/data/definitions/20.html


*   **CWE-89: SQL Injection**

    * **Description**: The application constructs SQL statements from user input, which attackers can manipulate to execute arbitrary SQL commands.
    * **Link**: https://cwe.mitre.org/data/definitions/89.html


*   **CWE-564: SQL Injection in ORM**

    * **Description**: An application using an Object-Relational Mapping (ORM) tool is vulnerable to SQL injection.
    * **Link**: https://cwe.mitre.org/data/definitions/564.html


*   **CWE-77: Command Injection**

    * **Description**: The application constructs operating system commands using user input, which attackers can manipulate to execute arbitrary commands.
    * **Link**: https://cwe.mitre.org/data/definitions/77.html


*   **CWE-78: Improper Neutralization of Special Elements used in an OS Command ('OS Command Injection')**

    * **Description**: The application constructs OS commands using user input without proper neutralization of special characters.
    * **Link**: https://cwe.mitre.org/data/definitions/78.html


*   **CWE-643: Improper Neutralization of Data within XPath Expressions ('XPath Injection')**

    * **Description**: The application constructs XPath queries from user input, which attackers can manipulate to alter the query's behavior.
    * **Link**: https://cwe.mitre.org/data/definitions/643.html


*   **CWE-74: Improper Neutralization of Special Elements in Output Used by a Downstream Component ('Injection')**

    * **Description**: The application uses user input in a way that it can affect downstream components, such as databases or command interpreters.
    * **Link**: https://cwe.mitre.org/data/definitions/74.html


*   **CWE-90: Improper Neutralization of Special Elements used in an LDAP Query ('LDAP Injection')**

    * **Description**: The application constructs LDAP queries from user input, which attackers can manipulate to alter the query's behavior.
    * **Link**: https://cwe.mitre.org/data/definitions/90.html


*   **CWE-917: Improper Neutralization of Special Elements used in an Expression Language Statement ('Expression Language Injection')**

    * **Description**: The application constructs Expression Language (EL) statements from user input, which attackers can manipulate to execute arbitrary code.
    * **Link**: https://cwe.mitre.org/data/definitions/917.html


* **CWE-352: Cross-Site Request Forgery (CSRF)**
  * **Description**: The application allows attackers to perform actions on behalf of authenticated users without their consent.
  * **Link**: https://cwe.mitre.org/data/definitions/352.html
