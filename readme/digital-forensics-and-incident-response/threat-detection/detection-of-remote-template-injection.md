---
icon: temperature-half
---

# Detection of Remote Template Injection

## Weaponized Microsoft Word Document with Embedded RTF Exploit

**Overview**

Weaponized Microsoft Word documents with embedded RTF (Rich Text Format) exploits are a common vector used by adversaries to deliver malware. These documents often exploit vulnerabilities in Microsoft Word or the underlying RTF processing libraries to execute arbitrary code on the target system. The embedded RTF exploit can be used to bypass security measures and deliver payloads such as malware, ransomware, or other malicious software.

**How It Works**

1. <mark style="color:green;">**Document Creation**</mark><mark style="color:green;">: The adversary creates a Microsoft Word document that contains an embedded RTF object. This RTF object is crafted to exploit a vulnerability in the RTF processing library.</mark>
2. <mark style="color:green;">**Exploit Delivery**</mark><mark style="color:green;">: The document is sent to the target via email, download link, or other means. When the target opens the document, the embedded RTF exploit is triggered.</mark>
3. <mark style="color:green;">**Payload Execution**</mark><mark style="color:green;">: The exploit executes arbitrary code, which can download and execute additional payloads, such as malware or ransomware.</mark>

**Example Scenario**

Imagine an adversary sends a phishing email to a target with a subject line like "Important Document for Review." The email contains a Microsoft Word attachment named "Important\_Document.docx." When the target opens the document, the embedded RTF exploit is triggered, and malware is downloaded and executed on the system.\


***

## Step-by-Step Demo

1. <mark style="color:green;">**Set Up the Environment**</mark><mark style="color:green;">:</mark>
   * <mark style="color:green;">Create a Microsoft Word document that contains an embedded RTF object.</mark>
   * <mark style="color:green;">Use a tool like</mark> <mark style="color:green;"></mark><mark style="color:green;">`rtfgen`</mark> <mark style="color:green;"></mark><mark style="color:green;">to generate a malicious RTF file.</mark>
2. <mark style="color:green;">**Create a Malicious RTF File**</mark><mark style="color:green;">:</mark>
   * <mark style="color:green;">Craft an RTF file that includes malicious code. For example, an RTF file that executes a command when opened.</mark>
3. <mark style="color:green;">**Embed the Malicious RTF File in a Word Document**</mark><mark style="color:green;">:</mark>
   * <mark style="color:green;">Insert the malicious RTF file into a Word document.</mark>
4. <mark style="color:green;">**Deliver the Document**</mark><mark style="color:green;">:</mark>
   * <mark style="color:green;">Send the document to a target system or open it in a controlled environment to observe the attack.</mark>

#### Example Code

**Generate a Malicious RTF File**

You can use a tool like `rtfgen` to generate a malicious RTF file. Here is an example of how to create a simple RTF file that includes a command:

```
from rtfgen import RtfDocument, RtfParagraph, RtfTextdef create_malicious_rtf(output_file):    doc = RtfDocument()    para = RtfParagraph()    para.add(RtfText("This is a malicious RTF file."))    para.add(RtfText("\\objdata \\objclass \\objemb \\objname \\objid \\objblip \\objext \\objbin"))    doc.add(para)    doc.write(output_file)create_malicious_rtf("malicious.rtf")
```

**Embed the Malicious RTF File in a Word Document**

1. <mark style="color:green;">Open Microsoft Word.</mark>
2. <mark style="color:green;">Insert the malicious RTF file as an object:</mark>
   * <mark style="color:green;">Go to</mark> <mark style="color:green;"></mark><mark style="color:green;">`Insert`</mark> <mark style="color:green;"></mark><mark style="color:green;">></mark> <mark style="color:green;"></mark><mark style="color:green;">`Object`</mark> <mark style="color:green;"></mark><mark style="color:green;">></mark> <mark style="color:green;"></mark><mark style="color:green;">`Create from File`</mark><mark style="color:green;">.</mark>
   * <mark style="color:green;">Browse to the</mark> <mark style="color:green;"></mark><mark style="color:green;">`malicious.rtf`</mark> <mark style="color:green;"></mark><mark style="color:green;">file and insert it into the document.</mark>
3. <mark style="color:green;">Save the Word document as</mark> <mark style="color:green;"></mark><mark style="color:green;">`malicious_document.docx`</mark><mark style="color:green;">.</mark>

**Deliver the Document**

<mark style="color:green;">Send the</mark> <mark style="color:green;"></mark><mark style="color:green;">`malicious_document.docx`</mark> <mark style="color:green;"></mark><mark style="color:green;">to a target system or open it in a controlled environment to observe the attack.</mark>



***

## REFERENCES

* [https://www.fortinet.com/blog/threat-research/cve-2017-11826-exploited-in-the-wild-with-politically-themed-rtf-document](https://www.fortinet.com/blog/threat-research/cve-2017-11826-exploited-in-the-wild-with-politically-themed-rtf-document)
* [https://attack.mitre.org/techniques/T1221/](https://attack.mitre.org/techniques/T1221/)

