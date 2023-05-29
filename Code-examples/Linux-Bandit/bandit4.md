## [Bandit4-5](https://overthewire.org/wargames/bandit/bandit5.html)

## Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. 

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
for i in $(ls); do file ./$i; done
```
```
file ./-file07
```
```
cat ./-file07
```

#### * copy password 

```
exit
```
#### * save password to Bandit/5
```
echo [password] > 5
```

```
sshpass -p $(cat 5) ssh bandit5@bandit.labs.overthewire.org -p 2220
```

