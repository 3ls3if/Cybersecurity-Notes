---
icon: envelope-open
---

# Gmail Address

## Introduction

Doxing is essentially gathering sensitive information about a target that they generally wouldn't want or expect disclosed. These details include everything from their name, email address, ZIP code, and even home and work addresses.

## [GHunt](https://github.com/mxrch/GHunt)

GHunt (v2) is an offensive Google framework, designed to evolve efficiently. It's currently focused on OSINT, but any use related with Google is possible

### Features

* CLI usage and modules
* Python library usage
* Fully async
* JSON export
* Browser extension to ease login

### Installation

```
$ pip3 install pipx
$ pipx ensurepath
$ pipx install ghunt
```

### Usage

First, launch the listener by doing `ghunt login` and choose between 1 of the 2 first methods:&#x20;

```
$ ghunt login

[1] (Companion) Put GHunt on listening mode (currently not compatible with docker)
[2] (Companion) Paste base64-encoded cookies
[3] Enter manually all cookies

Choice =>
```

Then, use GHunt Companion to complete the login.

The extension is available on the following stores :\
\
[![Firefox](https://camo.githubusercontent.com/5359aa1e74f28267b55ac077c0bb67497fafcbc99d84e2fbfd7a3642c57f4ca2/68747470733a2f2f66696c65732e636174626f782e6d6f652f3567326c64352e706e67)](https://addons.mozilla.org/en-US/firefox/addon/ghunt-companion/)   [![Chrome](https://camo.githubusercontent.com/e30d40727a6aa0ad0df1d59cf0cced20a8a8b47a6d650303dfadafab7e7f4a17/68747470733a2f2f73746f726167652e676f6f676c65617069732e636f6d2f7765622d6465762d75706c6f6164732f696d6167652f576c443877433667386b685957504a5573516365516b6858536c76312f55563443347962654254735a74343355347869732e706e67)](https://chrome.google.com/webstore/detail/ghunt-companion/dpdcofblfbmmnikcbmmiakkclocadjab)

{% hint style="info" %}
Copy the base64-encoded cookies and paste it in the ghunt terminal after choosing the option 2.
{% endhint %}

#### Getting Information of an Email

```
$ ghunt email <email_address>
```



***

## REFERENCES

* [https://docs.google.com/document/d/1WleGh4D3\_p7TYPhjfKRHQyMYwhZayYZayYY7AZSSzPs/edit?tab=t.0](https://docs.google.com/document/d/1WleGh4D3\_p7TYPhjfKRHQyMYwhZayYZayYY7AZSSzPs/edit?tab=t.0)
* [https://www.cybrary.it/blog/doxing-part-2](https://www.cybrary.it/blog/doxing-part-2)
* [https://github.com/mxrch/GHunt](https://github.com/mxrch/GHunt)
* [https://hacklido.com/blog/260-ghunt-20-gmail-osint-guide-part-1](https://hacklido.com/blog/260-ghunt-20-gmail-osint-guide-part-1)

