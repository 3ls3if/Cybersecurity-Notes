---
description: An evil RAT (Remote Administration Tool) for macOS / OS X.
icon: apple
---

# EvilOSX

### Features



* Emulate a terminal instance
* Simple extendable [module](https://github.com/Marten4n6/EvilOSX/blob/master/CONTRIBUTING.md) system
* No bot dependencies (pure python)
* Undetected by anti-virus (OpenSSL [AES-256](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) encrypted payloads)
* Persistent
* GUI and CLI support
* Retrieve Chrome passwords
* Retrieve iCloud tokens and contacts
* Retrieve/monitor the clipboard
* Retrieve browser history (Chrome and Safari)
* [Phish](https://i.imgur.com/x3ilHQi.png) for iCloud passwords via iTunes
* iTunes (iOS) backup enumeration
* Record the microphone
* Take a desktop screenshot or picture using the webcam
* Attempt to get root via local privilege escalation

### How To Use



```
# Clone or download this repository
$ git clone https://github.com/Marten4n6/EvilOSX

# Go into the repository
$ cd EvilOSX

# Install dependencies required by the server
$ sudo pip install -r requirements.txt

# Start the GUI
$ python start.py

# Lastly, run a built launcher on your target(s)
```

**Warning:** Because payloads are created unique to the target system (automatically by the server), the server must be running when any bot connects for the first time.

#### Advanced users



There's also a CLI for those who want to use this over SSH:

```
# Create a launcher to infect your target(s)
$ python start.py --builder

# Start the CLI
$ python start.py --cli --port 1337

# Lastly, run a built launcher on your target(s)
```

### Screenshots



[![CLI](https://camo.githubusercontent.com/6bc233352b90dc0a66a44c7f22d427d4e3c725dd5eac5e88217fd6bc49237bff/68747470733a2f2f692e696d6775722e636f6d2f44475943514d6c2e706e67)](https://camo.githubusercontent.com/6bc233352b90dc0a66a44c7f22d427d4e3c725dd5eac5e88217fd6bc49237bff/68747470733a2f2f692e696d6775722e636f6d2f44475943514d6c2e706e67) [![GUI](https://camo.githubusercontent.com/98156a7379dca488b43ec71a8d415315025ce4a335d6fcd0c150a23bb90c31d7/68747470733a2f2f692e696d6775722e636f6d2f7177336b347a342e706e67)](https://camo.githubusercontent.com/98156a7379dca488b43ec71a8d415315025ce4a335d6fcd0c150a23bb90c31d7/68747470733a2f2f692e696d6775722e636f6d2f7177336b347a342e706e67)

<br>

***

## REFERENCES

* [https://github.com/Marten4n6/EvilOSX](https://github.com/Marten4n6/EvilOSX)
* [https://www.youtube.com/watch?v=SkDz7NjifxA](https://www.youtube.com/watch?v=SkDz7NjifxA)
