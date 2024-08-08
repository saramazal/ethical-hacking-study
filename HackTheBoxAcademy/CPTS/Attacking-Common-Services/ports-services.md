## Common ports and services, along with tools for enumeration and example commands:


| **Port** | **Service**         | **Tools for Enumeration**                     | **Example Commands**                                                                 |
|----------|---------------------|-----------------------------------------------|--------------------------------------------------------------------------------------|
| **21**   | FTP (File Transfer Protocol) | `nmap`, `ftp`, `hydra`, `medusa`, `ncrack`      | `nmap -sV -p 21 $TARGET_IP` <br> `hydra -l user -P passlist.txt ftp://$TARGET_IP` |
| **22**   | SSH (Secure Shell)  | `nmap`, `ssh`, `hydra`, `medusa`, `ncrack`     | `nmap -sV -p 22 $TARGET_IP` <br> `hydra -l user -P passlist.txt ssh://$TARGET_IP`  |
| **25**   | SMTP (Simple Mail Transfer Protocol) | `nmap`, `smtp-user-enum`, `ncrack`, `hydra`     | `nmap -sV -p 25 $TARGET_IP` <br> `smtp-user-enum -M VRFY -U userlist.txt -t $TARGET_IP` |
| **53**   | DNS (Domain Name System) | `nmap`, `dig`, `dnsrecon`, `dnsenum`            | `nmap -sV -p 53 $TARGET_IP` <br> `dig @${TARGET_IP} example.com`                     |
| **80**   | HTTP (Web)          | `nmap`, `nikto`, `gobuster`, `dirb`, `whatweb` | `nmap -sV -p 80 $TARGET_IP` <br> `gobuster dir -u http://$TARGET_IP -w wordlist.txt` |
| **110**  | POP3 (Post Office Protocol) | `nmap`, `telnet`, `hydra`, `medusa`, `ncrack`    | `nmap -sV -p 110 $TARGET_IP` <br> `hydra -l user -P passlist.txt -s 110 $TARGET_IP pop3` |
| **139**  | NetBIOS/SMB (Server Message Block) | `nmap`, `smbclient`, `smbmap`, `crackmapexec`.`enum4linux` | `nmap -sV -p 139 $TARGET_IP` <br> `smbclient -L //$TARGET_IP` |
| **143**  | IMAP (Internet Message Access Protocol) | `nmap`, `telnet`, `hydra`, `medusa`, `ncrack` | `nmap -sV -p 143 $TARGET_IP` <br> `hydra -l user -P passlist.txt -s 143 $TARGET_IP imap` |
| **443**  | HTTPS (Web)         | `nmap`, `nikto`, `gobuster`, `sslscan`         | `nmap -sV -p 443 $TARGET_IP` <br> `sslscan $TARGET_IP`                               |
| **445**  | SMB/CIFS (Common Internet File System) | `nmap`, `smbclient`, `smbmap`, `enum4linux`, `rpcclient` | `nmap -sV -p 445 $TARGET_IP` <br> `smbmap -H $TARGET_IP`                            |
| **1433** | Microsoft SQL Server (MSSQL) | `nmap`, `sqsh`, `sqlcmd`, `hydra`, `ncrack`   | `nmap -sV -p 1433 $TARGET_IP` <br> `sqsh -S $TARGET_IP -U user -P password`         |
| **2121** | FTP (Alternate)     | `nmap`, `ftp`, `hydra`, `medusa`, `ncrack`      | `nmap -sV -p 2121 $TARGET_IP` <br> `ftp $TARGET_IP 2121`                            |
| **30021**| FTP (Custom)        | `nmap`, `ftp`, `hydra`, `medusa`, `ncrack`      | `nmap -sV -p 30021 $TARGET_IP` <br> `ftp $TARGET_IP 30021`                          |
| **3306** | MySQL               | `nmap`, `mysql`, `sqlmap`                      | `nmap -sV -p 3306 $TARGET_IP` <br> `mysql -u root -p -h $TARGET_IP`                 |
| **3389** | RDP (Remote Desktop Protocol) | `nmap`, `rdesktop`, `hydra`, `ncrack`          | `xfreerdp /v:$TARGETIP /u:$USER /pth:$HASH` <br> `rdesktop -u $USER -p '$PASS' $TARGET_IP`                            |
| **5432** | PostgreSQL          | `nmap`, `psql`, `hydra`, `medusa`              | `nmap -sV -p 5432 $TARGET_IP` <br> `psql -h $TARGET_IP -U user -d database`         |
| **8080** | HTTP-Proxy          | `nmap`, `nikto`, `gobuster`, `dirb`            | `nmap -sV -p 8080 $TARGET_IP` <br> `gobuster dir -u http://$TARGET_IP:8080 -w wordlist.txt` |
| **9001** | Tor                 | `nmap`, `telnet`, `curl`, `wget`               | `nmap -sV -p 9001 $TARGET_IP` <br> `telnet -l user $TARGET_IP 9001`                         |
| **2049** | NFS (Network File System) | `nmap`, `showmount`, `nfs-common`         | `nmap -sV -p 2049 $TARGET_IP` <br> `showmount -e $TARGET_IP`                        |
| **1521** | Oracle TNS (Transparent Network Substrate) | `nmap`, `tnscmd`, `hydra` | `nmap -sV -p 1521 $TARGET_IP` <br> `tnscmd ping -h $TARGET_IP`                      |
| **623**  | IPMI (Intelligent Platform Management Interface) | `nmap`, `ipmitool` | `nmap -sU -p 623 $TARGET_IP` <br> `ipmitool -I lanplus -H $TARGET_IP -U admin -P password chassis status` |
