---
icon: fax
---

# Investigating Favicon Hashes

## Introduction

Favicons are small icons in modern web applications that could be very useful for us in our day-to-day hunting activities, especially when we combine these icons with modern search engines to find assets on the internet.

## [FaviHunter](https://github.com/eremit4/favihunter)

This project aims to help a security professional find assets on the internet using favicon hashes on search engines such as [FOFA](https://en.fofa.info/), [Shodan](https://www.shodan.io/), [Censys](https://search.censys.io/), [Zoomeye](https://www.zoomeye.org/), [Criminal IP](https://www.criminalip.io/), and [ODIN](https://getodin.com/). The program returns a table with the custom queries of each search engine and their shortened URL with the query applied.

### Installation

```
git clone https://github.com/eremit4/favihunter.git

pip3 install -r requirements.txt
```

### Commands

```
# Help Menu
python3 favihunter.py --help

# Analyze a specific URL
python3 favihunter.py --url <url address>

# Analyze a file with URLs
python3 favihunter.py --urls-file <file path>

# Analyze a local favicon image
python3 favihunter.py --favicon <file path>

# Clean the local favicon directory
python3 favihunter.py --remove-favicons
```



<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption><p>Output</p></figcaption></figure>





***

## REFERENCES

* [https://github.com/eremit4/favihunter](https://github.com/eremit4/favihunter)









