# Manual Testing

- **Examine HTTP Headers and Responses**
    - **Tools**: `Burp Suite`, `Postman`, `Fiddler`
    - Analyze headers and responses for security misconfigurations.
- **SQL Injection Testing**
    - **Tools**: `sqlmap`, `Havij`
    - Check for SQL injection vulnerabilities.
    - Command Injection
    - LDAP Injection
    - XML External Entities (XXE)
- **Cross-Site Scripting (XSS) Testing**
    - Reflected XSS
    - Stored XSS
    - DOM-based XSS
    - **Tools**: `XSSer`, `Xenotix XSS Exploit Framework`
    - Test for XSS vulnerabilities.
- **Cross-Site Request Forgery (CSRF) Testing**
    - **Tools**: `Burp Suite`, `OWASP ZAP`
    - Check for CSRF vulnerabilities.
- **Authentication and Session Management Testing**
    - Brute force attacks
    - Credental stuffing
    - Session fixation
    - Insecure session handling
    - **Tools**: `Burp Suite`, `Postman`
    - Test login mechanisms, session tokens, and logout functionalities.
- **File Upload Testing**
    - Unrestricted file upload
    - Bypassing file type validation
    - Checking for execution of uploaded filed
    - **Tools**: `Burp Suite`, `OWASP ZAP`
    - Test for file upload vulnerabilities and verify file type restrictions.
- **Access Control Testing**
    - Testinf for Insecure Direct Object References (IDOR)
    - Privellege escalation
    - Horizontal and vertical access control testing
        
        **Tools**: `Burp Suite`, `Postman`
        
    - Verify proper access control and authorization mechanisms.
- Security Misconfigurations:
    - Default credentials
    - Exposed admin interfaces
    - Improperly configured security headers
- Sensitive Data Exposure:
    - Insecure storage (unencrypted data)
    - Insecure data transmission (lack of HTTPS)
    - Information leakage through error messages.