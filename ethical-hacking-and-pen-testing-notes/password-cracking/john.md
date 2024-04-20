# John

## Commands

### List Formats

```
john --list=formats
```

### Crack Sha1

```
john  --format=raw-sha1 hash.txt
```

### Crack Md5

```
john --format=raw-md5 hash.txt
```

### Cracking /etc/shadow

```
# Unshadow
unshadow passwd.txt shadow.txt > unshadowed.txt

# John
john /etc/shadow
```

### Wordlist

```
john --wordlist=<password.txt> /etc/shadow
```

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

## Cheat Sheet

{% embed url="https://haxez.org/wp-content/uploads/2022/07/HaXeZ_John_The_Ripper_Cheat_Sheet.pdf" %}
