# 🚪 Privilege Escalation

## Privilege Escalation Basics

#### Check for privileges

```
sudo -l
```

#### Login as another user

```
sudo -u user2 /bin/bash
```

#### Using SSH Private Key

```
nano id_rsa
chmod 600 id_rsa
ssh root@<ip address> -p 50706 -i id_rsa
```



## Privilege Escalation Advanced

