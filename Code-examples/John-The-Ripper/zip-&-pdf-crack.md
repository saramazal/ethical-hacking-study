# CTF TIP: How to unzip password protected zip file with pdf file password protected inside.
## [Kali Tools/John](https://www.kali.org/tools/john/)
## [Hashcat](https://hashcat.net/wiki/doku.php?id=example_hashes)
## [fcrackzip](https://www.kali.org/tools/fcrackzip/)

## Detailed Steps

1. 
```
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt <file.zip>  
PASSWORD FOUND!!!!: pw == **** *******
 unzip flag.zip
Archive:  flag.zip
[flag.zip] flag.pdf password:**** *******
password incorrect--reenter:
  inflating: flag.pdf
```

2.  Extract the Hash
Make sure you have pdf2john.py (usually found in the john/run directory if you have the full John the Ripper suite):

``` 
/usr/share/john/pdf2john.pl flag.pdf >  yourfile.hash
```

3. 

``` 
cat yourfile.hash: 
flag.pdf:$pdf$2*3*128*-1028*1*16*0fdcff65008750b48a459185119382b3*32*5ae0e1a58bd50f14924e2750cfc0ae 
```

4. Edit yourfile.hash file.

```
sudo nano yourfile.hash $pdf$2*3*128*-1028*1*16*0fdcff65008750b48a459185119382b3*32*5ae0e1a58bd50f14924e2750cfc0ae
```

5. Run John the Ripper
Use the hash file created in step 1 with John the Ripper:

 ```
 john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt yourfile.hash
 john --show yourfile.hash
 ```
 
6. or use 
```
hashcat -m 10500 yourfile.hash -a 0 /usr/share/wordlists/rockyou.txt --show
```

### Troubleshooting Tips
Ensure the PDF hash is correctly extracted: Verify the yourfile.hash is not empty.
Check John the Ripper's progress and logs: Sometimes John the Ripper might be running but not outputting directly to the terminal. Ensure it has time to process and check its logs.
Update John the Ripper: Ensure you have the latest version of John the Ripper installed.

