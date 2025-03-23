---
icon: binary-lock
---

# Decrypting Intermittent Encryption

## Introduction

Recently, a new trend has emerged in the world of ransomware: intermittent encryption, the partial encryption of targeted files. Many ransomware groups, such as BlackCat and Play, have adopted this approach. However, intermittent encryption is flawed.

## Intermittent Encryption

Intermittent encryption is when ransomware forgoes encrypting the entirety of every file, instead only encrypting part of each file, often blocks of a fixed size or only the beginning of targeted files.

There are several reasons attackers choose intermittent encryption over full encryption.

The most obvious is speed. Because files are only partially encrypted, intermittent encryption requires less time spent on each file, allowing the ransomware to impact more files in less time. This means that even if the ransomware is stopped before running to completion, more files will be encrypted, creating a more significant impact and making it more likely the ransomware will end up damaging critical files.

Moreover, encryption speed can also be used as a selling point. Ransomware providers can claim to have faster encryption to persuade affiliates to choose them over other providers.

Additionally, some security solutions make use of the amount of content being written to disk by a process in their heuristics to identify ransomware. With intermittent encryption, less content is written, and therefore, there is a smaller chance that ransomware will trigger such detections.

## Recovering Encrypted PDF

### [Whtie Phoenix](https://github.com/cyberark/White-Phoenix)

```
# Installation
git clone https://github.com/cyberark/White-Phoenix
cd White-Phoenix
pip3 install -r requirements.txt

# Run the tool
python3 White-Phoenix.py -f <pdf file name> -o <output directory>
```

{% hint style="info" %}
White Phoenix supports PDFs, Microsoft Office documents and zip files. But other formats, such as video and audio files, may also be recoverable.
{% endhint %}





## REFERENCES

* [https://www.cyberark.com/resources/threat-research-blog/white-phoenix-beating-intermittent-encryption](https://www.cyberark.com/resources/threat-research-blog/white-phoenix-beating-intermittent-encryption)
* [https://github.com/cyberark/White-Phoenix](https://github.com/cyberark/White-Phoenix)









