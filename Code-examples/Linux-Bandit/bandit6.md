## [Bandit6-7](https://overthewire.org/wargames/bandit/bandit7.html)

## Level Goal
The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size

```
find / -user bandit7 -group bandit6 -size 33c
```
```
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
```
cat /var/lib/dpkg/info/bandit7.password
```

#### * copy password 

```
exit
```
#### * save password to Bandit/7
```
echo [password] > 7
```

```
sshpass -p $(cat 7) ssh bandit7@bandit.labs.overthewire.org -p 2220
```
