---
icon: apple
---

# iOS Application Analysis

## Theory

### iOS Applications

The iOS application archive (.ipa extension) has a format and structure similar to the Android APK. Both are ZIP archives with a custom file extension containing all the necessary files for the application to function correctly. As visible in the following hex dump, the magic bytes of the IPA archive are the same as those of a typical ZIP header:

<figure><img src="../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

The application archive includes the application’s executable, configuration files, and any data or image resources. The common file types located in the archive, as described by Apple,  are as follows:&#x20;

• **Info.plist** The information property list file is the iOS version of the `AndroidManifest.xml` configuration file. It is a mandatory configuration file and contains information about the application such as permissions, supported platforms, and names of other relevant configuration files.&#x20;

• **Executable** A mandatory file that contains the application code.&#x20;

• **Resource files** Additional optional data files such as images and icons. These resources can be localized for a specific language or region or shared across them.&#x20;

• **Support files** Additional files that are not resources, such as private frameworks and plug-ins.

iOS applications, like macOS applications, are typically written in Objective- C or Swift programming languages.&#x20;

Objective-C is a general-purpose, object-oriented programming language that was used as the main language for developing applications on Apple platforms until the introduction of Swift in 2014.&#x20;

Swift is a successor of Objective-C and, among other things, brings simplicity, speed, and type safety while maintaining compatibility with both Objective-C and C.



***

## Practical

### Analyzing Binary Property List Files

{% hint style="info" %}
Property list files (.plist) store a serialized object representation of hierarchy objects and provide developers with a lightweight and portable way to store small amounts of data. These files can contain various data types, including arrays, dictionaries, strings, data, integers, floating-point values, or booleans.

\
Plist files can be stored either in XML or binary format. Because XML files are readable with any text editor, they are easy to open and analyze. Binary .plist files, however, need to be parsed or converted to XML format before they can be displayed in human-readable format.
{% endhint %}

#### Identify the format of .ipa file

```
file calculator.ipa
```

#### Unzip the iOS Application

```
unzip calculator.ipa
```

#### Identify the type of .plist file

```
file Info.plist
```

#### Convert .plist file from Binary to XML

```
plistutil -f xml -i Info.plist -o Info.xml
```

#### Read the .plist file

```
nano Info.xml
```



***

## REFERENCES

* [https://github.com/bitbar/test-samples/blob/master/apps/ios/calculator.ipa](https://github.com/bitbar/test-samples/blob/master/apps/ios/calculator.ipa)
* [https://github.com/iosre/iOSAppReverseEngineering](https://github.com/iosre/iOSAppReverseEngineering)
* [https://en.wikipedia.org/wiki/FBI%E2%80%93Apple\_encryption\_dispute](https://en.wikipedia.org/wiki/FBI%E2%80%93Apple\_encryption\_dispute)
* [https://developer.apple.com/library/content/documentation/CoreFoundati\
  CH101-SW1](https://developer.apple.com/library/content/documentation/CoreFoundatiCH101-SW1)
* [https://en.wikipedia.org/wiki/IOS\_version\_history#iOS\_9](https://en.wikipedia.org/wiki/IOS\_version\_history#iOS\_9.)
* [https://blog.lookout.com/pegasus-trident-cio-ciso-what-to-do/pegasus-trident-ios-update](https://blog.lookout.com/pegasus-trident-cio-ciso-what-to-do/pegasus-trident-ios-update)
* [https://osxdaily.com/2016/03/10/convert-plist-file-xml-binary-mac-os-x-plutil/](https://osxdaily.com/2016/03/10/convert-plist-file-xml-binary-mac-os-x-plutil/)
* [https://manpages.ubuntu.com/manpages/noble/man1/plistutil.1.html#:\~:text=DESCRIPTION,XML%20format%20or%20vice%2Dversa.](https://manpages.ubuntu.com/manpages/noble/man1/plistutil.1.html)
