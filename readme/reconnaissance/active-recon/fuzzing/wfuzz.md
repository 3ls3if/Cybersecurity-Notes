# ❄️ Wfuzz

## Installation

```
pip3 install wfuzz
```

## Commands

```
wfuzz -w <wordlist.txt> http://example.com/FUZZ

#Login bruteforce
wfuzz -z file,users.txt -d "username=FUZZ&password=FUZZ" http://example.com

#Basic auth
wfuzz -z file,users.txt --basic FUZZ:FUZZ http://example.com/FUZZ
```



***

## REFERENCES

* [https://book.hacktricks.xyz/pentesting-web/web-tool-wfuzz](https://book.hacktricks.xyz/pentesting-web/web-tool-wfuzz)
* [https://github.com/xmendez/wfuzz](https://github.com/xmendez/wfuzz)
* [https://wfuzz.readthedocs.io/en/latest/](https://wfuzz.readthedocs.io/en/latest/)
