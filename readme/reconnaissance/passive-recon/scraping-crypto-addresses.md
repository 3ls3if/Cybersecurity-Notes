# 🕷️ Scraping Crypto Addresses

## Spiderfoot

```
# installation
 git clone https://github.com/smicallef/spiderfoot.git
 cd spiderfoot
 pip3 install -r requirements.txt
 python3 ./sf.py -l 127.0.0.1:5001
```

## Scan for Bitcoin Addresses and Balances

```
python3 ./sf.py -m sfp_spider,sfp_bitcoin,sfp_blockchain -s websiteurl.com -F -q BITCOIN_ADDRESS,BITCOIN_BALANCE -q
```

## Scan for Ethereum Addresses

```
python3 ./sf.py -m sfp_spider,sfp_ethereum -s etherdonation.com -F ETHEREUM_ADDRESS -q
```



## REFERENCES

* [https://null-byte.wonderhowto.com/how-to/extract-bitcoin-wallet-addresses-balances-from-websites-with-spiderfoot-cli-0238107/](https://null-byte.wonderhowto.com/how-to/extract-bitcoin-wallet-addresses-balances-from-websites-with-spiderfoot-cli-0238107/)
* [https://github.com/smicallef/spiderfoot](https://github.com/smicallef/spiderfoot)

