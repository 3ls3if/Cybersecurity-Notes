# 🪟 Windows

## Live Data Collection

### Live Data Collection from Windows System

#### Create a Response Toolkit

It is critical to use trusted commands in all incident responses, irrespective of type of incident. An investigator should maintain a CD or a floppy that involves a minimum of the tools described below

```
cmd.exe
PsLoggedOn
rausers
netstat
Fport
PsList
ListDLLs
nbstat
Arp
Kill
md5sum
rmtshare
cryptcat
PsLogList
ipconfig
PsInfo
PsFile
PsService
auditpol
doskey
```

#### Saving Information Collected During Initial Response

There are four options available when the information has been retrieved from the live system:

* The information obtained from the hard drive of the target system should be saved.
* The obtained data should be noted by hand.
* The data obtained from the floppy disks or other external devices should be saved.
* The obtained data should be stored from forensic system by using cryptcat or Netcat.

#### Moving of Data using Netcat

```
# setup netcat listener on the forensic workstation
nc -l -p 2222 > pslist

# Run truested commands on the NT Server
pslist | nc <forensics workstation ip> 2222
```

#### Obtain Volatile Data

We need to retrieve temporal data from windows NT/2000 system before powering off the system. We collect the following temporal/volatile data before forensic duplication:

* The date and the time of the system.
* List of users that are currently logged on.
* Entire file system's time and date stamp.
* List of processes that are currently running.
* List of sockets that are open currently.
* Applications that are listening on the open sockets.
* List of systems that have current or had recent connections to the system.

#### Collect Temporal Data

```
# Run a trusted cmd.exe
Run the trusted version of cmd.exe from you own toolkit.

# Record system time and date
date > date.txt
time >> date.txt
type date.txt

# Identify logged on users and remote access users
loggedon

# Record Creation, Access time, Modification of Files
# Provide a recursive directory listing of all the access times on the C: drive
dir /t:a/a/s/o:dc:\

# Prove a recursive directory listing of all the modification times on the D: drive
dir /t:w/a/s/o:dd:\

# Provides a recursive directory listing of all the creation times on the E: drive
dir /t:c/a/s/o:de:\

# Identify Open Ports
netstat -an

# List of applications that are associated with those ports
fport

# List of current and recent connections
nbtstat -c

# Show the history of the commands
doskey /history
```



***

## REFERENCES

* [https://flylib.com/books/en/3.84.1.116/1/](https://flylib.com/books/en/3.84.1.116/1/)
* [https://github.com/g4xyk00/incident-response-toolkit](https://github.com/g4xyk00/incident-response-toolkit)
* [https://github.com/meirwah/awesome-incident-response](https://github.com/meirwah/awesome-incident-response)

