## [Bandit5-6](https://overthewire.org/wargames/bandit/bandit6.html)

## Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

```
ls
```

```
cd inhere
```
```
ls -l
```
```
ls -alR
```
```
find . -readable -size 1033c -not -executable
```

```
cat ./maybehere07/.file2
```

#### * copy password 

```
exit
```
#### * save password to Bandit/6
```
echo [password] > 6
```

```
sshpass -p $(cat 6) ssh bandit6@bandit.labs.overthewire.org -p 2220
```
