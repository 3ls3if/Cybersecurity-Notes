# 🦝 Installing and Configuring Network Based IDS In Ubuntu: Suricata

{% embed url="https://docs.suricata.io/en/latest/quickstart.html" %}

## Install Suricata In Ubuntu

```
$ sudo apt install suricata
```



## Modify The Configuration File

```
sudo gedit /etc/suricata/suricata.yaml
```

* In the Line no 15 Change the **HOME\_NET** IP address subnet to your machines IP subnet
* &#x20;In the Line no 580 change the **Interface** from eth0 to your local interface name (In my case it is enp0s3)
* In the Line no 661 change the **Interface** from eth0 to your local interface name (In my case it is enp0s3)
* In the Line no 129 change the **community-id** from **false** to **true**&#x20;
* You can add custom rules after Line no 1875

## Update Suricata

```
$ sudo suricata-update
```

## List Suricata Rules

```
$ sudo ls -al /var/lib/suricata/rules/
```

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

## Download Rulesets

```
$ sudo suricata-update list-sources
```

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

## Enable A Source

```
$ sudo suricata-update enable-source malsilo/win-malware
```

{% hint style="info" %}
**malsilo/win-malware** is the name of the source. You can choose any name after running  `sudo suricata-update list-sources`
{% endhint %}

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Update suricata after enabling a new source.
{% endhint %}



## Test The Suricata Configuration File

```
$ sudo suricata -T -c /etc/suricata/suricata.yaml -v
```

## Run Suricata

```
$ sudo systemctl start suricata.service
```

## View The Logs

```
$ ls -al /var/log/suricata
```



## Test If The Data Is Logged Or Not?

### Make a Curl Request

```
$ surl http://testmynids.org/uid/index.html
```

### View The Logs&#x20;

```
$ sudo cat /var/log/suricata/fast.log
```



## Suricata Custom Rules

### Create a Custom Rule

```
$ sudo gedit /etc/suricata/rules/local.rules
```

### Add the Below Line In local.rules file

```
alert icmp any any -> $HOME_NET (msg:"icmp ping"; sid:1; rev:1;)
```

### Add the local.rules file name/path in suricata.yaml file

* Add the below text after the Line no 1875 in suricata.yaml file

```
 - /etc/suricata/rules/local.rules
```

* Save the file and exit



## Install jq&#x20;

```
sudo apt-get install jq
```

## View the Latest Logs

```
$ sudo tail -f /var/log/suricata/eve.json | jq 'select(.event_type=="alert")'
```

