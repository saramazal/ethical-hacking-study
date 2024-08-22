# Official Write-Up for the Lucky Panther CTF TryHackMe 
#### luckypantherctf
## Task 1: Download the Image

Start by downloading the provided image file.

![luckypanther.jpg](https://github.com/saramazal/ethical-hacking-study/blob/main/CTF/luckypanther.jpg)

## Task 2: Investigate the Image

### Question 1: What Did You Find in the Picture?

**How:**

First, use the [steghide](https://www.kali.org/tools/steghide/) tool to analyze the image:

```bash
steghide info luckypanther.jpg
```

Output:

```plaintext
"luckypanther.jpg":
format: jpeg
capacity: 28.7 KB
Try to get information about embedded data? (y/n) y
Enter passphrase:
```

Since a passphrase is required, we need to find it. Let’s try [StegSeek](https://linux-packages.com/kali-linux/package/stegseek) with the `rockyou.txt` wordlist:

```bash
stegseek luckypanther.jpg /usr/share/wordlists/rockyou.txt -
```

StegSeek successfully finds the passphrase:

```plaintext
StegSeek 0.6 
[i] Found passphrase: "$pinkpanther"
```

Next, extract the hidden file using `steghide`:

```bash
steghide extract -sf luckypanther.jpg
```

Enter the passphrase `"$pinkpanther"` to extract the embedded file, which is `forest.zip`.

**Answer:** `forest.zip`

### Question 2: What is Your Second Find?

Let’s unzip the `forest.zip` file:

```bash
unzip forest.zip
```

Output:

```plaintext
Archive:  forest.zip
forest.zip: deepforest.pdf password:
```

The `forest.zip` file is password-protected. To crack it, use [fcrackzip](https://www.kali.org/tools/fcrackzip/):

```bash
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt forest.zip
```

After running the command, we find the password:

```plaintext
PASSWORD FOUND!!!!: pw == deepforest
```

Unzipping with the password `deepforest` reveals the `deepforest.pdf` file.

**Answer:** `deepforest.pdf`

### Question 3: What is Hiding in the Deep Forest?

Opening `deepforest.pdf` requires a password. To crack it, first extract the hash using `pdf2john`:

```bash
/usr/share/john/pdf2john.pl deepforest.pdf > deepforesthash
```

Then, use John the Ripper to crack the hash:

```bash
john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt deepforesthash
```

John successfully cracks the password:

```plaintext
good-luck (deepforest.pdf)
```

Alternatively, you can use [Hashcat](https://hashcat.net/wiki/doku.php?id=example_hashes). First, edit the hash file by removing `deepforest.pdf:` from the start, and save it as `deepforesthash2`.

To crack the hash with Hashcat:

```bash
hashcat -m 10500 deepforesthash2 -a 0 /usr/share/wordlists/rockyou.txt
```

Hashcat confirms the password is `good-luck`.

Now, open `deepforest.pdf` with the password `good-luck` to reveal the first flag.

**Answer:** `GUZ{U!_U4px3e!_l0h_4e3_va_4ur_Q33c_s0e3$g!_P0ate4g$!}`

## Task 3: What is the Flag?

Just a little more deciphering left.

*Are you in the Deep Forest?*

**Question: What is the Flag?**

We have a flag example from Task 2:

```plaintext
GUZ{U!_U4px3e!_l0h_4e3_va_4ur_Q33c_s0e3$g!_P0ate4g$!}
```

Using the **Cipher Identifier** tool at [dCode](https://www.dcode.fr/cipher-identifier), we identify it as a ROT13 cipher.
![image.png](https://github.com/saramazal/ethical-hacking-study/blob/main/CTF/rot13-1.png)

click on ROT-13 Cipher and decrypt srting:

![image.png](https://github.com/saramazal/ethical-hacking-study/blob/main/CTF/rot13-2.png)

We can decode it directly using ROT13, or by using [CyberChef](https://cyberchef.org/) with the ROT13 function.

**![image.png](https://github.com/saramazal/ethical-hacking-study/blob/main/CTF/rot13.png)

**Answer:** `THM{H!_H4ck3r!_y0u_4r3_in_4he_D33p_f0r3$t!_C0ngr4t$!}`

Great! Happy Hacking!

