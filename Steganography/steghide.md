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
steghide -info <file.name>
```
```
steghide extract -sf <file.name>
```
