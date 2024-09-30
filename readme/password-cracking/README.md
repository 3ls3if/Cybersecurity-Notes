# 🔓 Password Cracking

* ```
  hash-identifier [hash]
  ```
* ```
  john hashes.txt
  ```
* ```
  hashcat -m 500 -a 0 -o output.txt –remove hashes.txt /usr/share/wordlists/rockyou.txt
  ```
* ```
  hashcat -m 1000 dump.txt -o output.txt --remove -a 3 ?u?l?l?d?d?d?d
  ```
  * Brute force crack for NTLM hashes with an uppercase, lowercase, lowercase, and 4 digit mask
* List of hash types and examples for hashcat [https://hashcat.net/wiki/doku.php?id=example\_hashes ](https://hashcat.net/wiki/doku.php?id=example\_hashes)
* [https://hashkiller.co.uk](https://hashkiller.co.uk/) has a good repo of already cracked MD5 and NTLM hashes

#### **Bruteforcing:** <a href="#toc475368995" id="toc475368995"></a>

* ```
  hydra 10.0.0.1 http-post-form “/admin.php:target=auth&mode=login&user=^USER^&password=^PASS^:invalid” -P /usr/share/wordlists/rockyou.txt -l admin
  ```
* ```
  hydra -l admin -P /usr/share/wordlists/rockyou.txt -o results.txt IPADDR PROTOCOL
  ```
* ```
  hydra -P /usr/share/wordlistsnmap.lst 192.168.X.XXX smtp –V
  ```
  * Hydra SMTP Brute force

\
