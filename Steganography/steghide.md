## [steghide](https://www.kali.org/tools/steghide/)

 ```
sudo apt install steghide
 ```
 ```
steghide --help
 ```
 `for hide data:`
 
 ```
 steghide embed -cf <file.jpg> -ef <secret.txt>
 ```
 ```
 Enter passphrase:
 ```

`for extract:`
```
steghide -info <file.jpg>
```
```
steghide extract -sf <file.jpg>
```


`extra / brute-force without passphrase:`
```
for i in $(cat /usr/share/wordlists/rockyou.txt); do echo '[+] Trying ' $i; steghide extract -sf <file.jpg> --passphrase $i; done   
```
