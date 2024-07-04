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



## SSH Tunneling

### Local Port Forwarding or Local Tunneling

```
# Machine which has blocked port 3389
ssh -L 8181:<ssh server ip>:3389 <username>@<ssh server ip>
```



### Dynamic Port Forwarding or Dynamic Tunneling

```
# Machine which has blocked web traffics
ssh -D 8081 <username>@<ssh server ip> 

# Set the proxy in the browser 
localhost:8081
```



### Reverse Port Forwarding or Reverse Tunneling

```
# Windows Machine
ssh -R 8081:localhost:3389 <username>@<ssh server ip>

# Attacker Machine
RDP using username as localhost and port as 3389
```

