# 🔐 SSH Commands

## Connect to a host using SSH

```
# Basic Connection
ssh <username>@<host ip> -p <port number>

# If no matching host key type found error is given
ssh -p <port> <username>@<host ip> -o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedAlgorithms=+ssh-rsa

# Using a keyfile
ssh -p <port> -i <keyfile> <username>@<host ip>
```

