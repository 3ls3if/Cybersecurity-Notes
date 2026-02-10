---
icon: windows
---

# Office365 Phishing - Browser in the Browser

## Office365 Phishing - Browser in the Browser



**GitHUB:** [https://github.com/jakedmurphy1/O365-BITB?tab=readme-ov-file](https://github.com/jakedmurphy1/O365-BITB?tab=readme-ov-file)

This repo contains a fake two-part Office365 login implemented within a Browser-In-The-Browser attack window. It can be used on a web server that supports PHP files. Any entered credentials are saved in _/opt/O365-BITB/creds.txt_. After logging in, the victim is redirected to an Office365 error page. Follow steps below for a quick and easy setup.



#### Get Started

Run the below commands in the /var/www/html folder of your web server.

```
git clone https://github.com/jakedmurphy1/O365-BITB.git
```

```
cd O365-BITB
```

```
chmod 666 creds.txt
```

Move the credentials file into a non-public folder:

```
mkdir /opt/O365-BITB && mv creds.txt /opt/O365-BITB/creds.txt
```

Then visit _/O365-BITB/index.html_ in your browser and give it a try! Any gathered credentials will be stored in _/opt/O365-BITB/creds.txt_

#### Watch Creds in Real Time

You can watch credentials appear in real-time with a little bash magic:

```
tail -f /opt/O365-BITB/creds.txt | while read line; do echo $line; sleep 3; done
```

#### Sources

{% embed url="https://github.com/mrd0x/BITB" %}



***

## REFERENCES

* [https://github.com/jakedmurphy1/O365-BITB?tab=readme-ov-file](https://github.com/jakedmurphy1/O365-BITB?tab=readme-ov-file)
