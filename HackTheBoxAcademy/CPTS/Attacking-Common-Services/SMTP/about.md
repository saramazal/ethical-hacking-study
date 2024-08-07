# SMTP Service Overview

## What is SMTP?
The Simple Mail Transfer Protocol (SMTP) is a protocol used for sending and receiving email messages between servers. It operates at the application layer of the TCP/IP protocol suite and uses a client-server model to transfer email reliably and efficiently.

## Ports Used by SMTP
- **Port 25**: Default port for SMTP communication.
- **Port 587**: Used for SMTP with STARTTLS (for secure communication).
- **Port 465**: Deprecated port for SMTP over SSL (SMTPS).

## SMTP Enumeration
SMTP enumeration involves probing the SMTP server to gather information about valid email addresses and user accounts. This can help in identifying potential targets for phishing or brute-force attacks.

### Tools for SMTP Enumeration
- **smtp-user-enum**: Enumerates users by sending VRFY, EXPN, and RCPT TO commands.
  ```sh
  smtp-user-enum -M RCPT -U userlist.txt -D example.com -t $TARGET_IP
  ```
- **Metasploit Framework**: Provides auxiliary modules for SMTP enumeration.
  ```sh
  use auxiliary/scanner/smtp/smtp_enum
  ```

## Tools for Attacking SMTP
- **Hydra**: Brute-force tool for various protocols including SMTP.
  ```sh
  hydra -l user@example.com -P passwords.txt -s 587 -S $TARGET_IP smtp
  ```
- **Medusa**: Another brute-force tool for SMTP and other services.
  ```sh
  medusa -h $TARGET_IP -U userlist.txt -P passwords.txt -M smtp -n 587 -T 5
  ```
- **Metasploit Framework**: Includes modules for exploiting SMTP vulnerabilities.
  ```sh
  use exploit/unix/smtp/exim4_string_format
  ```

## How to Prevent SMTP Vulnerabilities
1. **Disable VRFY and EXPN Commands**: Prevent user enumeration by disabling these commands on the SMTP server.
2. **Use Strong Authentication**: Implement strong, multi-factor authentication for accessing the SMTP server.
3. **Enable TLS/SSL**: Ensure that SMTP communication is encrypted using TLS/SSL on ports 587 or 465.
4. **Rate Limiting and Account Lockout**: Implement rate limiting and account lockout policies to mitigate brute-force attacks.
5. **Regular Audits and Updates**: Regularly audit the SMTP server configuration and keep the software updated to patch known vulnerabilities.

By following these best practices, you can enhance the security of your SMTP server and reduce the risk of attacks.
