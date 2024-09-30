---
icon: bee
---

# OWASP BWAPP Setup

## Introduction

bWAPP, or a _buggy web application_, is a free and open source deliberately insecure web application.\
It helps security enthusiasts, developers and students to discover and to prevent web vulnerabilities.\
bWAPP prepares one to conduct successful penetration testing and ethical hacking projects.

## Docker Pull

```
docker pull raesene/bwapp
```

## Docker Run

```
docker run -d -p 80:80 raesene/bwapp
```

{% hint style="info" %}
**Visit:** `http://127.0.0.1:80/install.php`
{% endhint %}



***

## REFERENCES

* [https://hub.docker.com/r/raesene/bwapp/](https://hub.docker.com/r/raesene/bwapp/)
* [http://www.itsecgames.com/](http://www.itsecgames.com/)
