# 🐧 Unix/Linux

## Live Data Collection from UNIX System

The main goal of live data collection is to obtain temporal or volatile data before forensic dumplication. The scope of initial response can be expanded by obtaining configuration files, system files, files that contain attacker's tools and suspicious programs, and log files to confirm quickly whether the event has occured or not.

Recovering deleted files in the UNIX system becomes a major difference in working with UNIX and Windows. In Windows, files that correspond to the running process from the hard drive cannot be deleted, whereas in UNIX, program files can be deleted even if the process is running.

### Create a Response Toolkit

It is difficult to create a trusted toolkit as it takes a lot of time; the reason behind this is that every variable in UNIX required a UNIX toolkit, In some cases, you may need to compile a source code on your own because some recommended tools are not included with the official UNIX system.

### Saving Information Obtained at the Time of Initial Response

The storage options are:

* Save the data on local hard drive.
* Save the data on external devices such as USB or tape drives.
* Record the information manually (i.e. by hand).
* To transfer the retrieved data to the forensic workstations, use Netcat or Cryptcat.

### Obtain Volatile Data Before Forensic Duplication

#### Collecting the Data

* Date and time of the system.
* A list of users who are currently logged on.
* Entire file system's time and date stamps.
* List of processes that are currently in running state.
* List of currently open sockets.
* List of application that is listening to those open ports.
* List of systems that have current or recent connections to the system.

```
# Run a Trusted shell

# Mount Trusted Toolkit
mount /dev/fd0 /mnt/floppy

# Record time and date of the system
date

# Identify who is currently logged on to the system
w

# Record creation, alteration, and access time of each file
ls -alRu / > /floppy/atime
ls -alRc / > /floppy/ctime
ls -alR / > /floppy/mtime

# Identify Open Ports
netstat -an

# Enlist applications associated with open ports
netstat -anp

# Identify the Running Processes
ps -aux

# Record Cryptographic Checksum
md5sum * > md5sums.txt
```

#### Storing Information Obtained During Initial Response

Following shows the binary log files of particular interest:

* Utmp file accessed with w command.
* Wtmp file accessed with last utility.
* Last log file accessed with last log utility.
* Process accounting logs accessed with lastcomm utility.

Some ASCII text log files are:

* Xferlog
* Web access logs
* History files

#### Obtian Important Configuration Files

The configuration files commonly accessed or modified by attackers are maintained by UNIX. To locate unauthorized user IDs and unauthorized trusted relationships of these configuration files are important to be reviewed. Here is the list about which file should be obtained during initial response:

* To look for unauthorized user accounts:  /etc/passwd
* To ensure about password authentication of every account: /etc/shadow
* To look for escalation in scope of access and privilege: /etc/groups
* To list the DNS (Domain Name System) entries: /etc/hosts
* To review trusted relationships: /etc/hosts.equiv
* To look in the start-up files: /etc/rc
* To list scheduled events: crontab files

#### Dumping System RAM

There is no proper way to dump the system RAM on the UNIX system. We normally transfer `/proc/kmem` or `/proc/kcore` file from the target system. These files contain the files of the system RAM in discontinuous manner. Core dump type of analysis can be done by very few people.



***

## REFERENCES

* [https://flylib.com/books/en/3.84.1.117/1/](https://flylib.com/books/en/3.84.1.117/1/)
* [https://github.com/meirwah/awesome-incident-response](https://github.com/meirwah/awesome-incident-response)

