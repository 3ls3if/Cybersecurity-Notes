# 🔢 Enumeration Cheatsheet

#### **General Enumeration:**

* ```
  nmap -vv -Pn -A -sC -sS -T 4 -p- 10.0.0.1
  ```
  * Verbose, syn, all ports, all scripts, no ping
* ```
  nmap -v -sS -A -T4 x.x.x.x
  ```
  * Verbose, SYN Stealth, Version info, and scripts against services.
* ```
  nmap –script smb-check-vulns.nse –script-args=unsafe=1 -p445 [host]
  ```
  * Nmap script to scan for vulnerable SMB servers – WARNING: unsafe=1 may cause knockover
* ```
  netdiscover -r 192.168.1.0/24
  ```

#### **FTP Enumeration (21):** <a href="#toc475368978" id="toc475368978"></a>

* ```
  nmap –script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 10.0.0.1
  ```

#### **SSH (22):** <a href="#toc475368979" id="toc475368979"></a>

* ```
  ssh INSERTIPADDRESS 22
  ```

#### **SMTP Enumeration (25):** <a href="#toc475368980" id="toc475368980"></a>

* ```
  nmap –script smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 10.0.0.1
  ```
* ```
  nc -nvv INSERTIPADDRESS 25
  ```
* ```
  telnet INSERTIPADDRESS 25
  ```

#### **Finger Enumeration (79):** <a href="#toc494187363" id="toc494187363"></a>

Download script and run it with a wordlist: [http://pentestmonkey.net/tools/user-enumeration/finger-user-enum](http://pentestmonkey.net/tools/user-enumeration/finger-user-enum)

#### **Web Enumeration (80/443):** <a href="#toc475368981" id="toc475368981"></a>

* dirbuster (GUI)
* ```
  dirb http://10.0.0.1/
  ```
* ```
  nikto –h 10.0.0.1
  ```

#### **Pop3 (110):** <a href="#toc475368982" id="toc475368982"></a>

* ```
  telnet INSERTIPADDRESS 110
  ```
* ```
  USER [username]
  ```
* ```
  PASS [password]
  ```
  * To login
* ```
  LIST
  ```
  * To list messages
* ```
  RETR [message number]
  ```
  * Retrieve message
* ```
  QUIT
  ```
  * quits

#### **RPCBind (111):** <a href="#toc475368983" id="toc475368983"></a>

* ```
  rpcinfo –p x.x.x.x
  ```

#### **SMB\RPC Enumeration (139/445):** <a href="#toc475368984" id="toc475368984"></a>

* ```
  enum4linux –a 10.0.0.1
  ```
* `nbtscan x.x.x.x`
  * Discover Windows / Samba servers on subnet, finds Windows MAC addresses, netbios name and discover client workgroup / domain
* ```
  py 192.168.XXX.XXX 500 50000 dict.txt
  ```
* ```
  python /usr/share/doc/python-impacket-doc/examples/samrdump.py 192.168.XXX.XXX
  ```
* ```
  nmap IPADDR --script smb-enum-domains.nse,smb-enum-groups.nse,smb-enum-processes.nse,smb-enum-sessions.nse,smb-enum-shares.nse,smb-enum-users.nse,smb-ls.nse,smb-mbenum.nse,smb-os-discovery.nse,smb-print-text.nse,smb-psexec.nse,smb-security-mode.nse,smb-server-stats.nse,smb-system-info.nse,smb-vuln-conficker.nse,smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-regsvc-dos.nse
  ```
* ```
  smbclient -L //INSERTIPADDRESS/
  ```
  * List open shares
* ```
  smbclient //INSERTIPADDRESS/ipc$ -U john
  ```

#### **SNMP Enumeration (161):** <a href="#toc475368985" id="toc475368985"></a>

* ```
  snmpwalk -c public -v1 10.0.0.0
  ```
* ```
  snmpcheck -t 192.168.1.X -c public
  ```
* ```
  onesixtyone -c names -i hosts
  ```
* ```
  nmap -sT -p 161 192.168.X.X -oG snmp_results.txt
  ```
* ```
  snmpenum -t 192.168.1.X
  ```

#### **Oracle (1521):** <a href="#toc475368986" id="toc475368986"></a>

* ```
  tnscmd10g version -h INSERTIPADDRESS
  ```
* ```
  tnscmd10g status -h INSERTIPADDRESS
  ```

#### **Mysql Enumeration (3306):** <a href="#toc475368987" id="toc475368987"></a>

* ```
  nmap -sV -Pn -vv  10.0.0.1 -p 3306 --script mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122
  ```

#### **DNS Zone Transfers:** <a href="#toc475368988" id="toc475368988"></a>

* ```
  nslookup -> set type=any -> ls -d blah.com
  ```
* ```
  dig axfr blah.com @ns1.blah.com
  ```
  * This one works the best in my experience
* ```
  dnsrecon -d TARGET -D /usr/share/wordlists/dnsmap.txt -t std --xml ouput.xml
  ```

#### **Mounting File Share** <a href="#toc475368989" id="toc475368989"></a>

* ```
  showmount -e IPADDR
  ```
* ```
  mount 192.168.1.1:/vol/share /mnt/nfs  -nolock
  ```
  * mounts the share to /mnt/nfs without locking it
* ```
  mount -t cifs -o username=user,password=pass,domain=blah //192.168.1.X/share-name /mnt/cifs
  ```
  * Mount Windows CIFS / SMB share on Linux at /mnt/cifs if you remove password it will prompt on the CLI (more secure as it wont end up in bash\_history)
* ```
  net use Z: \\win-server\share password  /user:domain\janedoe /savecred /p:no
  ```
  * Mount a Windows share on Windows from the command line
* ```
  apt-get install smb4k –y
  ```
  * Install smb4k on Kali, useful Linux GUI for browsing SMB shares

#### **Fingerprinting:  Basic versioning / finger printing via displayed banner** <a href="#toc475368990" id="toc475368990"></a>

* ```
  nc -v 192.168.1.1 25
  ```
* ```
  telnet 192.168.1.1 25
  ```

#### **Exploit Research** <a href="#toc475368991" id="toc475368991"></a>

* ```
  searchsploit windows 2003 | grep -i local
  ```
  * Search exploit-db for exploit, in this example windows 2003 + local esc

#### **Compiling Exploits** <a href="#toc475368992" id="toc475368992"></a>

* ```
  gcc -o exploit exploit.c
  ```
  * Compile C code, add –m32 after ‘gcc’ for compiling 32 bit code on 64 bit Linux
* ```
  i586-mingw32msvc-gcc exploit.c -lws2_32 -o exploit.exe
  ```
  * Compile windows .exe on Linux

#### **Packet Inspection:** <a href="#toc475368993" id="toc475368993"></a>

* ```
  tcpdump tcp port 80 -w output.pcap -i eth0
  ```
  * tcpdump for port 80 on interface eth0, outputs to output.pcap

\
