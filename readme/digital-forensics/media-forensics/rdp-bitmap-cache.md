---
icon: laptop-arrow-down
---

# RDP Bitmap Cache

## Theory

### What is RDP bitmap cache?

When a user connects to another system using RDP, small size (bitmap) images are stored in their RDP profile files, so that once the same image is to be used in the session it can be fetched/pulled quicker. And the overall RDP session experience is enhanced in case of a slow connection. This artifact can help us sometimes in identifying what was the user seeing in their RDP sessions.

### RDP bitmap cache location

```
C:\Users\<username>\AppData\Local\Microsoft\Terminal Server Client\Cache
```



***

## Practical

### [BMC Viewer Backup](https://github.com/0xTowel/BMC-Viewer-Backup) (Windows)

```
# Run bitmapcacheviewer.exe in windows
.\bitmapcacheviewer.exe

# Select the .bmc file
Click on Browse and select the .bmc file

Click on Load
```

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Bitmapcacheviewer Output</p></figcaption></figure>



### [BMC-Tools](https://github.com/ANSSI-FR/bmc-tools) (Linux)

```
# Run bmc-tools.py
python bmc-tools.py -s "/home/ubuntu/Downloads/file.bmc" -d RDPBitMapOutput -b
```

* \-s : Specify the BMCache file or directory to process
* \-d : Specify the directory where to store the extracted bitmaps
* \-b : Will provide one bitmap image which aggregates all bitmap images



***

## REFERENCES

* [https://hejelylab.github.io/blog/IRC/RDP-Bitmap-Cache](https://hejelylab.github.io/blog/IRC/RDP-Bitmap-Cache)
* [https://github.com/ANSSI-FR/bmc-tools](https://github.com/ANSSI-FR/bmc-tools)
* [https://github.com/0xTowel/BMC-Viewer-Backup](https://github.com/0xTowel/BMC-Viewer-Backup)
* [https://en.wikipedia.org/wiki/BMP\_file\_format](https://en.wikipedia.org/wiki/BMP\_file\_format)
* [https://security.opentext.com/appDetails/RDP-Cached-Bitmap-Extractor](https://security.opentext.com/appDetails/RDP-Cached-Bitmap-Extractor)
* [https://learn.microsoft.com/en-us/answers/questions/430008/remote-desktop-cache-permanently-caching-bitmaps](https://learn.microsoft.com/en-us/answers/questions/430008/remote-desktop-cache-permanently-caching-bitmaps)

