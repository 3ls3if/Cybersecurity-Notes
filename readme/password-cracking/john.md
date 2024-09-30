# John

## Commands

### Formats

```
john --list=formats
```

### Crack SHA1

```
john  --format=raw-sha1 hash.txt
```

### Crack MD5

```
john --format=raw-md5 hash.txt
```

### Cracking Shadow Files

<pre><code># Unshadow
unshadow passwd.txt shadow.txt > unshadowed.txt

# John
john /etc/shadow

<strong># Wordlist
</strong>john --wordlist=&#x3C;password.txt> /etc/shadow
</code></pre>

### Cracking Zip Files

```
# Zip to John
zip2john file.zip > ziphash.txt

# John
john --format=zip ziphash.txt
```

### Crack .pfx File

```
pfx2john <pfx file> > hash.txt

john hash.txt --wordlist=<wordlist location>
```

### Crack GPG Passphrase

**Read More** [Here](https://blog.atucom.net/2015/08/cracking-gpg-key-passwords-using-john.html)

```
gpg2john priv.key > hash 

john hash --wordlist=/usr/share/wordlists/rockyou.txt 
```

### Crack SSH Passphrase

```
ssh2john /home/chinju/.ssh/id_rsa > ssh_hash.txt

john ssh_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

***

## REFERENCES

* [https://blog.atucom.net/2015/08/cracking-gpg-key-passwords-using-john.html](https://blog.atucom.net/2015/08/cracking-gpg-key-passwords-using-john.html)
* [https://cheatsheet.haax.fr/passcracking-hashfiles/john\_cheatsheet/](https://cheatsheet.haax.fr/passcracking-hashfiles/john\_cheatsheet/)
* [https://countuponsecurity.com/wp-content/uploads/2016/09/jtr-cheat-sheet.pdf](https://countuponsecurity.com/wp-content/uploads/2016/09/jtr-cheat-sheet.pdf)
* [https://null-byte.wonderhowto.com/how-to/crack-ssh-private-key-passwords-with-john-ripper-0302810/](https://null-byte.wonderhowto.com/how-to/crack-ssh-private-key-passwords-with-john-ripper-0302810/)
