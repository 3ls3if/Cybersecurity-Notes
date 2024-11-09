---
icon: duck
---

# BlueDucky Script

## Introduction

{% hint style="info" %}
🚨 CVE-2023-45866 - BlueDucky Implementation (Using DuckyScript) 🔓 Unauthenticated Peering Leading to Code Execution (Using HID Keyboard)
{% endhint %}

BlueDucky is a powerful tool for exploiting a vulnerability in Bluetooth devices. By running this script, you can:

1. 📡 Load saved Bluetooth devices that are no longer visible but have Bluetooth still enabled.
2. 📂 Automatically save any devices you scan.
3. 💌 Send messages via ducky script format to interact with devices.

## Installation

```
# update apt
sudo apt-get update
sudo apt-get -y upgrade

# install dependencies from apt
sudo apt install -y bluez-tools bluez-hcidump libbluetooth-dev \
                    git gcc python3-pip python3-setuptools \
                    python3-pydbus

# install pybluez from source
git clone https://github.com/pybluez/pybluez.git
cd pybluez
sudo python3 setup.py install

# build bdaddr from the bluez source
cd ~/
git clone --depth=1 https://github.com/bluez/bluez.git
gcc -o bdaddr ~/bluez/tools/bdaddr.c ~/bluez/src/oui.c -I ~/bluez -lbluetooth
sudo cp bdaddr /usr/local/bin/
```

### Running the Script

```
git clone https://github.com/pentestfunctions/BlueDucky.git
cd BlueDucky
sudo hciconfig hci0 up
python3 BlueDucky.py
```

Alternatively,

```
pip3 install -r requirements.txt
```

## Demo

{% embed url="https://github.com/pentestfunctions/BlueDucky/blob/main/images/BlueDucky.gif" %}



***

## REFERENCES

* [https://github.com/pentestfunctions/BlueDucky](https://github.com/pentestfunctions/BlueDucky)
* [https://www.linkedin.com/feed/update/urn:li:activity:7183695755906289664/](https://www.linkedin.com/feed/update/urn:li:activity:7183695755906289664/)
* [https://github.com/marcnewlin/hi\_my\_name\_is\_keyboard](https://github.com/marcnewlin/hi\_my\_name\_is\_keyboard)



