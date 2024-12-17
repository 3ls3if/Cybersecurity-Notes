---
icon: unlock-keyhole
---

# Decrypt SSL Traffic

## Introduction

You can decrypt SSL traffic using the SSL session keys. One method to do this is by setting the SSLKEYLOGFILE environment variable to a filename on the client operating system to log the SSL key information. This method is useful under any of the following conditions:

* Due to security reasons, you can only log the SSL session key of one user.
* You have no access to, or you do not want to run commands on, the BIG-IP system.

You can use this method to decrypt both RSA as well as Diffie-Hellman-based key exchanges (such as DHE or ECDHE).



{% hint style="success" %}
You must meet the following prerequisites to use this procedure:

* You are using either the Firefox or Chrome browsers on the client system to access a web application.
* You have Wireshark installed on the client system.
{% endhint %}



***

## Log the SSL Session Keys in Linux

To log the SSL session keys on Linux by setting the SSLKEYLOGFILE, perform the following procedure:

**Impact of procedure:** Performing the following procedure should not have a negative impact on your system.

1. Log in to Linux.
2. Close all Firefox and Chrome browsers.
3. Open a terminal for command line access.
4.  Set the SSLKEYLOGFILE environment variable for your account by using the following command syntax:

    export SSLKEYLOGFILE="/home/\<account\_name>/sslkeyfile"

    For example:

    export SSLKEYLOGFILE="/home/user1/sslkeyfile"
5. Start a packet capture using an application such as Wireshark or **tcpdump**. For information about **tcpdump** refer to [K411: Overview of packet tracing with the tcpdump utility](https://my.f5.com/manage/s/article/K411).
6.  Start Firefox or Chrome from the same terminal.

    For example:

    Firefox &

    **Note**: You must start the browser from the same command terminal because the session variable is set only on the terminal.
7. Access a web application and perform the steps you want to troubleshoot. As you do this, the SSL session keys are logged in the file you specified in Step 4.
8. Stop the packet capture and save the file to your client system.

{% hint style="success" %}
**Note**: After you perform the **Uploading the SSL key log file in Wireshark** procedure and review the decrypted packet capture file, you can delete the SSL log file to revert your changes by entering the following command: **export SSLKEYLOGFILE=""**.
{% endhint %}

## Load the SSL key log file in Wireshark

1. Open Wireshark on your client system.
2.  Go to **Edit** > **Preferences** > **Protocols** > **TLS**.

    **Note**: For Wireshark versions earlier than 3.0.0, go to **Edit** > **Preferences** > **Protocols** > **SSL**. For Mac go to **Wireshark** > **Preferences** > **Protocols** > **TLS**.
3. For the **(Pre)-Master-Secret log filename**, select **Browse** and locate the SSL log file you created.
4. Select **OK**.
5. Open the packet capture file in Wireshark.
6. In the Wireshark packet window, select previously encrypted packets to view unencrypted application data.

**Load the SSL key log file in Tshark (the command-line version of Wireshark)**

1.  Specify the **tls.keylog\_file:\<file>** option on the Tshark command line. For example:

    tshark -o 'tls.keylog\_file:logfile.pms' -r capture.pcap



***

## REFERENCES

* [https://my.f5.com/manage/s/article/K50557518#OnLinux](https://my.f5.com/manage/s/article/K50557518#OnLinux)
* [https://www.youtube.com/watch?v=bU61cDtMsNU\&ab\_channel=SathvikTechtuber](https://www.youtube.com/watch?v=bU61cDtMsNU\&ab_channel=SathvikTechtuber)





