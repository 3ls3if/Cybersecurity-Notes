---
description: Tracking USB events with USBRip.
icon: usb
---

# USB Event Tracking

## Introduction

[**usbrip**](https://github.com/snovvcrash/usbrip) (inherited from "USB Ripper", not "USB R.I.P.") is a simple forensics tool with command line interface that lets you keep track of USB device artifacts (i.e., USB event history) on Linux machines.

## Installation

```bash
sudo -H python3 -m pip install -U usbrip
usbrip -h

OR

pipx install usbrip

OR

sudo apt install python3-venv p7zip-full -y
git clone https://github.com/snovvcrash/usbrip && cd usbrip
sudo -H installers/install.sh
cd
usbrip -h

OR

sudo apt install usbrip
```

## Usage

```bash
# ---------- BANNER ----------

~$ usbrip banner
Get usbrip banner.

# ---------- EVENTS ----------

~$ usbrip events history [-t | -l] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [-c <COLUMN> [<COLUMN> ...]] [-f <FILE> [<FILE> ...]] [-q] [--debug]
Get USB event history.

~$ usbrip events open <DUMP.JSON> [-t | -l] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [-c <COLUMN> [<COLUMN> ...]] [-q] [--debug]
Open USB event dump.

~$ sudo usbrip events genauth <OUT_AUTH.JSON> [-a <ATTRIBUTE> [<ATTRIBUTE> ...]] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [-f <FILE> [<FILE> ...]] [-q] [--debug]
Generate a list of trusted (authorized) USB devices.

~$ sudo usbrip events violations <IN_AUTH.JSON> [-a <ATTRIBUTE> [<ATTRIBUTE> ...]] [-t | -l] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [-c <COLUMN> [<COLUMN> ...]] [-f <FILE> [<FILE> ...]] [-q] [--debug]
Get USB violation events based on the list of trusted devices.

# ---------- STORAGE ----------

~$ sudo usbrip storage list <STORAGE_TYPE> [-q] [--debug]
List contents of the selected storage. STORAGE_TYPE is either "history" or "violations".

~$ sudo usbrip storage open <STORAGE_TYPE> [-t | -l] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [-c <COLUMN> [<COLUMN> ...]] [-q] [--debug]
Open selected storage. Behaves similarly to the EVENTS OPEN submodule.

~$ sudo usbrip storage update <STORAGE_TYPE> [IN_AUTH.JSON] [-a <ATTRIBUTE> [<ATTRIBUTE> ...]] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [--lvl <COMPRESSION_LEVEL>] [-q] [--debug]
Update storage -- add USB events to the existing storage. COMPRESSION_LEVEL is a number in [0..9].

~$ sudo usbrip storage create <STORAGE_TYPE> [IN_AUTH.JSON] [-a <ATTRIBUTE> [<ATTRIBUTE> ...]] [-e] [-n <NUMBER_OF_EVENTS>] [-d <DATE> [<DATE> ...]] [--host <HOST> [<HOST> ...]] [--vid <VID> [<VID> ...]] [--pid <PID> [<PID> ...]] [--prod <PROD> [<PROD> ...]] [--manufact <MANUFACT> [<MANUFACT> ...]] [--serial <SERIAL> [<SERIAL> ...]] [--port <PORT> [<PORT> ...]] [--lvl <COMPRESSION_LEVEL>] [-q] [--debug]
Create storage -- create 7-Zip archive and add USB events to it according to the selected options.

~$ sudo usbrip storage passwd <STORAGE_TYPE> [--lvl <COMPRESSION_LEVEL>] [-q] [--debug]
Change password of the existing storage.

# ---------- IDs ----------

~$ usbrip ids search [--vid <VID>] [--pid <PID>] [--offline] [-q] [--debug]
Get extra details about a specific USB device by its <VID> and/or <PID> from the USB ID database.

~$ usbrip ids download [-q] [--debug]
Update (download) the USB ID database.
```



***

## REFERENCES

* [https://github.com/snovvcrash/usbrip](https://github.com/snovvcrash/usbrip)
* [https://www.youtube.com/watch?v=Pag0FJfsyu0\&ab\_channel=NullByte](https://www.youtube.com/watch?v=Pag0FJfsyu0\&ab\_channel=NullByte)



