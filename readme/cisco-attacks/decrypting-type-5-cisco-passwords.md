# Decrypting Type 5 Cisco Passwords

## Theory

This password type was introduced around 1992 and it is essentially a 1,000 iteration of MD5 hash with salt. The salt is 4 characters long (32 bits). For modern computers this is not difficult enough and thus in many cases it can be successfully cracked.

The following example shows type 5 password found in a Cisco configuration:

```
username administrator secret 5 $1$mERr$yhf7f2RnC74CxKANvoekD.

enable secret 5 $1$mERr$A419.HL58lq743wXS4kSM1
```



***

## Practical

### Decrypt Cisco Type 5 Passwords with John

John the Ripper recognizes this password type as **md5crypt**. To crack it, we have to again first convert it to the following john friendly format and save it in a file:

```
administrator:$1$mERr$yhf7f2RnC74CxKANvoekD.
secret:$1$mERr$A419.HL58lq743wXS4kSM1
```

Then we can crack it like this using a dictionary, for example:

```
john --format=md5crypt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```



### Decrypt Cisco Type 5 Password with Hashcat

Hashcat recognizes this password type as hash mode **500**. To crack it, we can keep using the same john friendly format. Then we can crack it like this using a dictionary, for example:

```
hashcat -m 500 --username -O -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

Note that by using the `-O` parameter (optimized kernels), we will greatly increase the speed. But it will also limit the password length to 31 characters.



***

## REFERENCES

* [https://www.infosecmatter.com/cisco-password-cracking-and-decrypting-guide/](https://www.infosecmatter.com/cisco-password-cracking-and-decrypting-guide/)
* [https://www.petenetlive.com/KB/Article/0000940](https://www.petenetlive.com/KB/Article/0000940)
* [https://community.cisco.com/t5/network-management/enable-secret-privilege-password/td-p/4441088](https://community.cisco.com/t5/network-management/enable-secret-privilege-password/td-p/4441088)
