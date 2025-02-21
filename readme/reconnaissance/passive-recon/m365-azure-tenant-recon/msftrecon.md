---
icon: toolbox
---

# MSFTRecon

## Introduction

MSFTRecon is a reconnaissance tool designed for red teamers and security professionals to map Microsoft 365 and Azure tenant infrastructure. It performs comprehensive enumeration without requiring authentication, helping identify potential security misconfigurations and attack vectors.

## Installation

```
# Clone the repository
git clone https://github.com/yourusername/msftrecon.git
cd msftrecon

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

### Usage

Basic scan:

```
./msftrecon.py -d example.com
```

JSON output:

```
./msftrecon.py -d example.com -j
```

Government cloud:

```
./msftrecon.py -d example.gov --gov
```

China cloud:

```
./msftrecon.py -d example.cn --cn
```

### Sample Output

```
[+] Target Organization:
Tenant Name: Contoso
Tenant ID: 1234abcd-1234-abcd-1234-1234abcd1234

[+] Federation Information:
Namespace Type: Managed
Brand Name: Contoso
Cloud Instance: microsoftonline.com

[+] Azure AD Configuration:
Tenant Region: NA

[+] Azure AD Connect Status:
  Identity Configuration: Managed (Cloud Only)
  Authentication Type: Managed

  [!] Identity Insights:
  * Cloud-only authentication detected
  * All authentication handled in Azure AD
  * Focus on cloud-based attack vectors
```



***

## REFERENCES

* [https://github.com/Arcanum-Sec/msftrecon](https://github.com/Arcanum-Sec/msftrecon)

