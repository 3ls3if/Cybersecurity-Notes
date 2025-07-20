# 🦈 How To Convert Windows netsh Event Trace Log (ETL) Files For Wireshark Analysis

## How To Convert Windows netsh Event Trace Log (ETL) Files For Wireshark Analysis

{% hint style="warning" %}
This article documents how to use, download, and then convert network trace files captured by the Microsoft Windows netsh native network trace tool. This is a companion article for the video "How To Convert netsh Event Trace Log ETL Files For Wireshark Analysis".
{% endhint %}

### Issue

Boomi Technical Support often requires a network trace to further analyze a customer's issue that is related to network traffic, i.e., no response from Boomi API, a Boomi connector time out, or an unknownHostException, etc., reported in Process Reporting.  These errors can be investigated further by obtaining a network capture.   Microsoft Windows provides a native tool that captures traffic and other events from a Windows OS/server, however, the generated file is not readable by all network analysis tools, for example, [wireshark](http://www.wireshark.org/about.html), the leading industry network analysis tool.

### Environment

Windows OS servers use Network shell ([**netsh**](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc754753\(v=ws.10\))), a native command-line utility that allows you to configure and display the status of various network communications server roles and components installed, to specifically provide network traffic captures.

With netsh there is nothing to install on the Windows server, and it has the ability to persist tracing across reboots, with circular logging capability as well. \
\
[netsh](https://learn.microsoft.com/en-us/windows/win32/ndf/using-netsh-to-manage-traces) creates a native Event Trace Log (.etl) file that can be read by [Microsoft Network Monitor 3.4 ](https://learn.microsoft.com/en-us/windows/win32/ndf/using-network-monitor-to-view-etl-files)application or the file can be converted to a capture file (.cap) format, which wireshark can open and interpret/analyze.&#x20;

Note that Microsoft Network Monitor 3.4 must be downloaded from the [Microsoft archive site](http://www.microsoft.com/en-us/download/details.aspx?id=4865), whereas netsh is native to the OS.

### Capture Tool

The following netsh command is a typical use case, for a non-filtered trace file, capturing all events and network traffic on the local server.  Other examples, like this Microsoft [article](https://techcommunity.microsoft.com/t5/iis-support-blog/capture-a-network-trace-without-installing-anything-amp-capture/ba-p/376503) can also be used for reference, as well as this [web article](https://chentiangemalc.wordpress.com/2012/02/22/netsh-traceuse-it/).\
\
`netsh trace start capture=yes tracefile=%temp%\%computername%_nettrace.etl`

\
Run the following netsh command from an elevated (administrator) command prompt:\
\
`netsh trace start capture=yes tracefile=%temp%\%computername%_nettrace.etl maxsize=200 filemode=circular overwrite=yes report=no`\
\
netsh can limit the trace file to a circular network capture that will not exceed 200 MB in size.  A size limit is used (_maxsize_) to limit the capture file size.  The _filemode_ specifies which file mode is applied when tracing output is generated: single|circular|append. If unspecified, the default entry “fileMode=circular”.   \
\
If the network trace is short in duration, less than two to five (2 to 5) minutes, no maxsize is required usually.  fileMode=circular and maxsize are used typically when a network trace is required over a longer span of time or for intermittently re-occurring errors.



### Conversion Tools

#### etl2pcapng

A tool to convert the netsh output file (.etl) to a wireshark readable file (.pcap or .pcapng) is the [etl2pcapng](https://github.com/microsoft/etl2pcapng/releases) tool.  Download etl2pcapng to a folder on the server to use it for converting .elt files to .pcapng files, readable by Wireshark.&#x20;

Usage instructions are listed [here](https://github.com/microsoft/etl2pcapng). \
\
In a Windows command window, change directory (cd) to the folder where the etl2pcapng.exe application is downloaded.\
\
1\.  Enter the following command:\
\
`etl2pcapng sample_nettrace.etl converted.nettrace.pcap`\
\
<mark style="color:green;">\<Results></mark>\ <mark style="color:green;">IF: medium=eth                  ID=0    IfIndex=3       VlanID=0</mark>\ <mark style="color:green;">Converted 10276 frames</mark>\
\
2\.  Now open the file converted.nettrace.pcap with wireshark or another analysis tool, like Network Monitor, discussed below.\
&#x20;

#### Network Monitor&#x20;

[Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/4865) application can be used, both to capture Windows network traffic and analyze the packets captured, discussed [here](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/collect-data-using-network-monitor). \
\
Network Monitor can also read the native Event Trace Log (.etl) file that is created by netsh or convert the .etl file to a readable (.cap) format, which wireshark can open and interpret/analyze as well.\
\
Launch the Network Monitor application, after download and installation, and open a .etl file.. or use filters to capture TCP traffic.\
\
Reference:

Please also review the "[How To Convert netsh Event Trace Log ETL Files For Wireshark Analysis](https://www.youtube.com/watch?v=KG1g3itHkio)" video for a live demonstration of this article.



***

## REFERENCES

* [https://community.boomi.com/s/article/How-To-Convert-Windows-netsh-Event-Trace-Log-ETL-Files-For-Wireshark-Analysis](https://community.boomi.com/s/article/How-To-Convert-Windows-netsh-Event-Trace-Log-ETL-Files-For-Wireshark-Analysis)
