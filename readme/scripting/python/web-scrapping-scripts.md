---
icon: scroll
---

# Web Scrapping Scripts

## Scrapping Bug Bounty Sites

```python
import requests
from bs4 import BeautifulSoup

# URL to scrape
url = "https://www.vulnerability-lab.com/list-of-bug-bounty-programs.php"

# Set headers to mimic a browser request
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like>
}

# Send a GET request with headers
response = requests.get(url, headers=headers)
if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
        tables = soup.find_all('table')
        a_tags = tables[4].find_all('a')
        sites_list = open('bug-bounty-list.txt', 'w')

        for a in a_tags:
                #print(a)
                sites_list.write(a.get('href')+'\n')
else:
    print(f"Failed to retrieve content. Status code: {response.status_code}")

```

## Getting the Domains

```python
site_list = open('bug-bounty-list.txt', 'r')
sites = site_list.readlines()

domain_list = open('bug-bounty-domains.txt', 'w')

for site in sites:
        if not 'mailto' in site:
                split_site = site.split('/')
                if len(split_site)>1:
                        domain_list.write(split_site[2]+'\n')

```

## Getting the Keywords

```python
import tldextract

domain_list = open('bug-bounty-domains.txt', 'r')
word_list = open('bug-bounty-wordlist.txt', 'w')

for domain in domain_list.readlines():
        tld = tldextract.extract(domain)
        word_list.write(tld.domain+'\n')
```

