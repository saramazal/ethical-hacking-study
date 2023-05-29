## [Bandit0-1](https://overthewire.org/wargames/bandit/bandit0.html)

### The Bandit wargame  can help you to learn and practice security concepts in the form of fun-filled games.

## Bandit Level 0
Level Goal
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

```
pwd
```

```
mkdir Bandit
```
```
cd Bandit
```
### * save password [bandit0] to Bandit/0
```
echo bandit0 > 0
```
```
sshpass -p $(cat 0) ssh bandit0@bandit.labs.overthewire.org -p 2220
```
```
ls
```
```
cat readme
```
#### * copy password from readme
```
exit
```
#### * save password to Bandit/1
```
echo [password] > 1
```

```
sshpass -p $(cat 1) ssh bandit1@bandit.labs.overthewire.org -p 2220
```

