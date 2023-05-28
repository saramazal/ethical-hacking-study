## [Kali Tools/John](https://www.kali.org/tools/john/)
## [John Docs](https://www.openwall.com/john/)
## [John Github](https://github.com/openwall/john)
## [freeCodeCamp Tutorial](https://www.freecodecamp.org/news/crack-passwords-using-john-the-ripper-pentesting-tutorial/)


```
 sudo apt install john
 ```
 
 ```
 john -h
 ```
 ```
 john --list=formats
 ```
 ```
 john --format=<hash-format> <hashes.txt>
 ```
 
 ```
 john --format=<hash-format> --wordlist=/usr/share/wordlists/rockyou.txt <hash_to_crack.txt> 
 ```
Unshadow  for John

```
unshadow /path/to/passwd /path/to/shadow > <output-file>
```    
 
