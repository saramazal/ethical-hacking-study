SMTP (Simple Mail Transfer Protocol) and port 110 (commonly associated with POP3, Post Office Protocol version 3) are both used in the email communication process, but they serve different purposes and operate on different ports.

### SMTP vs. POP3

- **SMTP (Port 25, 587, 465)**:
  - **Purpose**: Used for sending and relaying email messages from a client to an email server or between servers.
  - **Operation**: Handles the outgoing mail process. When you send an email, SMTP is responsible for transmitting the message from the sender’s email client to the recipient's email server.

- **POP3 (Port 110)**:
  - **Purpose**: Used for retrieving and downloading email messages from a mail server to a client.
  - **Operation**: Handles the incoming mail process. When you check your email, POP3 allows you to download emails from the server to your email client, where they are typically stored locally.

### Connection Between SMTP and Telnet on Port 110

**Telnet** is a protocol used to remotely access and manage network devices and services. When accessing an email server via Telnet on port 110, you are interacting with the POP3 service.

Here's how they fit into the email system:

1. **Sending Email (SMTP)**:
   - Email clients or servers use SMTP to send messages to an email server.
   - SMTP operates over ports 25, 587, or 465.

2. **Receiving Email (POP3)**:
   - After an email is received by the mail server via SMTP, users can retrieve it using POP3.
   - POP3 operates over port 110.

### Example Use of Telnet with POP3

When you connect to an email server using Telnet on port 110, you are accessing the POP3 service to download emails. For example:

```sh
telnet $TARGET_IP 110
```

You would then issue POP3 commands to interact with the mail server, such as:

- **USER**: To specify the username.
- **PASS**: To specify the password.
- **LIST**: To list messages in the mailbox.
- **RETR**: To retrieve a specific message.

### Summary

- **SMTP** is used for sending emails and operates on ports 25, 587, or 465.
- **POP3** is used for retrieving emails and operates on port 110.
- **Telnet** on port 110 allows you to interact with the POP3 service to manage incoming emails.

While SMTP and POP3 are different protocols used for different stages of email communication, they are interconnected in the overall process of sending and receiving emails.
