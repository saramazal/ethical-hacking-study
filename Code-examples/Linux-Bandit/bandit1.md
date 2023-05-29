## [Bandit1](https://overthewire.org/wargames/bandit/bandit2.html)

## Level Goal
The password for the next level is stored in a file called - located in the home directory

```
ls
```

```
cat ./-
```

### * copy password 

```
exit
```
### * save password to to Bandit/2
```
echo [password] > 2
```

```
sshpass -p $(cat 2) ssh bandit2@bandit.labs.overthewire.org -p 2220
```





