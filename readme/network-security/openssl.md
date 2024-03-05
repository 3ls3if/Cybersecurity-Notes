# 🏛️ OpenSSL

## Commands

### List Ciphers

```
openssl list -cipher-commands
```

### Base64

```
echo "Hello World" > plain.txt

# Encoding
openssl enc -base64 -in plain.txt

# Saving the output
openssl enc -base64 -in plain.txt -out cipher.txt

# Decoding
openssl enc -base64 -d in cipher.txt
```

### AES 128

```
# Encryption
openssl enc -aes-128-cbc -in plain.txt -out cipher
<Enter a password>

# Decryption
openssl enc -aes-128-cbc -d -in cipher -out cipher-dec.txt
```

### RSA

```
# Generate RSA Keys
openssl genrsa -out keypair 2048

# Extract public key from the private key
openssl rsa -in keypair -pubout

# Get detailed information
openssl rsa -in keypair -text
```

### Encrypted Linux Passwd

```
# You can add this encrypted password in /etc/passwd
openssl passwd Password123

# Generate Salted Password
openssl passwd -1 -salt User123 Password123
```
