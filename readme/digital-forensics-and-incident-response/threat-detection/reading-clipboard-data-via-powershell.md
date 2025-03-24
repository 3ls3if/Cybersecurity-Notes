---
icon: square-terminal
---

# Reading Clipboard Data via Powershell

## Clipboard Data

Adversaries may collect data stored in the clipboard from users copying information within or between applications.

For example, on Windows adversaries can access clipboard data by using `clip.exe` or `Get-Clipboard`.[\[1\]](https://msdn.microsoft.com/en-us/library/ms649012)[\[2\]](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/clip)[\[3\]](https://www.cisa.gov/uscert/ncas/alerts/aa21-200b) Additionally, adversaries may monitor then replace users’ clipboard with their data (e.g., [Transmitted Data Manipulation](https://attack.mitre.org/techniques/T1565/002)).[\[4\]](https://blog.reversinglabs.com/blog/mining-for-malicious-ruby-gems)

macOS and Linux also have commands, such as `pbpaste`, to grab clipboard contents.[\[5\]](https://medium.com/rvrsh3ll/operating-with-empyre-ea764eda3363)



{% hint style="success" %}
ID: T1115Sub-techniques:  No sub-techniques

ⓘTactic: [Collection](https://attack.mitre.org/tactics/TA0009)

ⓘPlatforms: Linux, Windows, macOSVersion: 1.2

Created: 31 May 2017

Last Modified: 14 April 2023
{% endhint %}

## Commands

**Windows**

* `clip`
* `echo "New Clipboard Text" | clip`
* `Get-Clipboard`

**macOS**

* `pbpaste`

**Linux**

* `xclip -o`
* `echo "New Clipboard Text" | xclip`
* `xsel --clipboard --output`
* `echo "New Clipboard Text" | xsel --clipboard --input`



***

## REFERENCES

* [https://attack.mitre.org/techniques/T1115/](https://attack.mitre.org/techniques/T1115/)



