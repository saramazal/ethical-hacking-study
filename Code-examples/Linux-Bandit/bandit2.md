## [Bandit2-3](https://overthewire.org/wargames/bandit/bandit3.html)

## Level Goal
The password for the next level is stored in a file called spaces in this filename located in the home directory.

```
ls
```

```
cat spaces\ in\ this\ filename
```

### * copy password 

```
exit
```
### * save password to to Bandit/3
```
echo [password] > 3
```

```
sshpass -p $(cat 3) ssh bandit3@bandit.labs.overthewire.org -p 2220
```