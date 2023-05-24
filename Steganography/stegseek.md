`for download` [stegseek/releases](https://github.com/RickdeJager/stegseek/releases)

```
sudo apt install ./stegseek_0.6-1.deb
```
`for hide data:`

```
stegseek –embed <file.txt> <file.jpg> 
Enter passphrase: ... 
```
`detection:`

```
time stegseek –seed <file.jpg>
```

`cracking:`

```
stegseek <file.jpg> /usr/share/wordlists/rockyou.txt -
```

