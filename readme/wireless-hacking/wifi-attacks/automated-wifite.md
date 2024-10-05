# Automated: Wifite

## What is Wifite

Wifite is a wireless auditing tool developed by Derv82 and maintained by kimocoder. You can find the original repository [here](https://github.com/kimocoder/wifite2). In the latest Kali Linux, it comes pre-installed. It’s a great alternative to the more tedious to use wireless auditing tools and provides simple CLI to interact and perform wireless attacks. It has great features like 5GHz support, Pixie Dust attack, WPA/WPA2 handshake capture attack and PMKID attack as well.

## Basic Commands

```
# Help Menu
wifite -h

# Check connected AP
wifite -i wlan0

# Check other access points running on the same channel
wifite -c 10

# Scan for more than one channel
wifite -c 10,6

# Display access points only clients connected
wifite --clients-only
```

## WPA/WPA2 Handshake Capture

```
# Start wifite
wifite --skip-crack

# Now follow the menu driven options to capture the handshake
```

## More  Attack Commands

```
# Custom Dictionary attack
wifite --dict /root/dict.txt

# Mac Spoofing
wifite --random-mac
```







## REFERENCES

* [https://www.hackingarticles.in/wireless-penetration-testing-wifite/](https://www.hackingarticles.in/wireless-penetration-testing-wifite/)
* [https://www.macvendorlookup.com/](https://www.macvendorlookup.com/)
