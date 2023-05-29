## [Bandit3-4](https://overthewire.org/wargames/bandit/bandit4.html)

## Level Goal
The password for the next level is stored in a hidden file in the inhere directory.

```
ls
```

```
cd inhere
```
```
ls -la
```
```
cat .hidden
```

### * copy password 

```
exit
```
### * save password to to Bandit/4
```
echo [password] > 4
```

```
sshpass -p $(cat 4) ssh bandit4@bandit.labs.overthewire.org -p 2220
```