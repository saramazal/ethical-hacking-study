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

```sudo nmap -sV -sC $TARGET_IP -Pn```
![nmap-scan]](/workspace/ethical-hacking-study/HackTheBoxAcademy/CPTS/Attacking-Common-Services/ftp-nmap-scan.png)

2. What username is available for the FTP server? 

3. Use the discovered username with its password to login via SSH and obtain the flag.txt file. Submit the contents as your answer. 

## Solution:
1. 