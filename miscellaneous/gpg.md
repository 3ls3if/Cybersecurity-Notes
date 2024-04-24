# 🔒 GPG

## Theory

gpg is the OpenPGP (Pretty Good Privacy) part of the GNU Privacy Guard (GnuPG). It is a tool to provide digital encryption and signing services using the OpenPGP standard. gpg features complete key management and all the bells and whistles you would expect from a full OpenPGP implementation.

The gpg utility has a lot of options, but fortunately for us, encrypting and decrypting are easy to do and only require that you know three options for quick use: Create or encrypt (`-c`), decrypt (`-d`), and extract and decrypt (no option).



***

## Practical

### Encrypt a file

The quick method for encrypting a file is to issue the `gpg` command with the `-c` (create) option:

```
echo This is an encryption test > file1.txt

gpg -c file1.txt

file file2.txt.gpg

mv file2.txt.gpg testfile01.doc

file testfile01.doc
```

### Decrypt a file

If you want to extract the original file while decrypting it, strangely enough, you issue the `gpg` command with no options.

```
gpg cfile.txt.gpg 
```

### Decrypt using  key

```
gpg --import b_secret.asc

gpg --decrypt b_txt.pgp
```



***

## REFERENCES

* [https://superuser.com/questions/920793/how-to-specify-private-key-when-decrypting-a-file-using-gnupg](https://superuser.com/questions/920793/how-to-specify-private-key-when-decrypting-a-file-using-gnupg)
* [https://www.redhat.com/sysadmin/encryption-decryption-gpg](https://www.redhat.com/sysadmin/encryption-decryption-gpg)
* [https://www.tecmint.com/gpg-encrypt-decrypt-files/](https://www.tecmint.com/gpg-encrypt-decrypt-files/)
