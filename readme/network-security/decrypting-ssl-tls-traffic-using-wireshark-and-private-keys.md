---
icon: lock-keyhole-open
---

# Decrypting SSL/TLS traffic using Wireshark and private keys

{% hint style="danger" %}
**Important**: Decrypting the SSL application data may expose sensitive information, such as credit card numbers and passwords. It is  recommended that you do not provide private keys to a third party.
{% endhint %}

## Wireshark

The SSL dissector in Wireshark allows you to decrypt application data. This feature is helpful for network troubleshooting or packet and performance analysis.

### Prerequisites

You must meet the following prerequisites to use this procedure:

* Your Wireshark software is compiled against GnuTLS (SSL decryption support).
* The RSA private key file is in PEM format.

{% hint style="success" %}
**Note**: You cannot decrypt Diffie-Hellman Ephemeral (DHE) key exchanges. Therefore, traffic using these ciphers will not be decoded.
{% endhint %}

### Procedures

**Decrypting SSL/TLS traffic using Wireshark and private keys**

1. Open the **Wireshark** utility.
2. Open the capture file containing the encrypted SSL/TLS traffic.
3. Open the **Preferences** window by navigation to **Edit** > **Preferences**.
4. Expand **Protocols** and click **TLS**.\
   **Note:** In the older versions of Wireshark (2.x and older) navigate to **SSL** instead of TLS.
5. You can redirect SSL debug by specifying a file location in the **TLS Debug file** text box.
6. To specify the RSA private key, click **Edit** and then click **+** and enter the following information:
   * **IP address**: The IP address of the SSL server in IPv4 or IPv6 format
   * **Port**: The port number
   * **Protocol**: A protocol name for the decrypted network data
   * **Key File**: Path to the RSA private key
   * **Password**: Specify the password for PCKS#12 keystore
7. Click **OK**.

For more information, refer to the [Wireshark TLS wiki](https://wiki.wireshark.org/TLS).



***

## REFERENCES

* [https://my.f5.com/manage/s/article/K19310681](https://my.f5.com/manage/s/article/K19310681)
* [https://isc.sans.edu/diary/Psst+Your+Browser+Knows+All+Your+Secrets+/16415](https://isc.sans.edu/diary/Psst+Your+Browser+Knows+All+Your+Secrets+/16415)
