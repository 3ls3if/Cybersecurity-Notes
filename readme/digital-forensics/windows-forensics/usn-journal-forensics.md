---
icon: newspaper
---

# USN Journal Forensics

## Introduction

NTFS is the default journaling file system for windows operating systems. Understanding NTFS features and how it works helps Digital Forensics investigators navigate and conduct their analysis for various objectives. The NTFS file system contains several files (called metafiles) to organize and structure the file system, one of those metafiles is the master file table ($MFT) which is used by forensics practitioners to gain insight into all files within an NTFS structured volume. Later, Microsoft added the USN Journal (Update Sequence Number) “$UsnJrnl” metafile which is also called the change journal, to maintain information of all changes occurred to files and folders on an NTFS volume, providing records for what and when changes are made and to which objects.

One USN Journal is stored within each NTFS volume and is stored in the NTFS metafile named “$Extend\\$UsnJrnl”. The journal begins with an empty file, and whenever a change is made to the volume, a record is added to the file. Each record will contain a 64-bit Update Sequence Number (USN), the name of the file and a bit flag (e.g. USN\_REASON\_DATA\_OVERWRITE) representing the change that was made.

“$UsnJrnl” has two main data streams which are, “**$J**”which records file and folder changes that occurred on the volume, and “**$MAX**”which is a small file that stores metadata about “$UsnJrnl”.

## Benefits in Forensics

Since “**$J**” has records of all changes on files and folders in a volume including deleted files, this opens the doors for digital forensics investigators and threat hunters to empower their analysis with information such as the following:

* Detection of malicious tools and bad files that were present at some point in time within the file system, which provides insight into suspicious/malicious user activity.
* Detection of “Timestomping” activity, a technique used by attackers which is the alteration of timestamps of files to confuse investigators during their analysis.
* Extending “Prefetch” artifacts value, which each contain the dates for the last 8 times an executable was run, which is a limitation of the artifact. This limitation can be overcome to gain the dates for more executions of an executable (Subject to the limitations of USN Journal below).

## Tools

* [https://github.com/jschicht/UsnJrnl2Csv/blob/master/UsnJrnl2Csv64.exe](https://github.com/jschicht/UsnJrnl2Csv/blob/master/UsnJrnl2Csv64.exe)
* [https://github.com/EricZimmerman/MFTECmd](https://github.com/EricZimmerman/MFTECmd)

[MFTECmd](https://github.com/EricZimmerman/MFTECmd) Usage\



<figure><img src="https://images.squarespace-cdn.com/content/v1/60d08f10063a3d3fb6875391/65f2a68a-fa09-48aa-92ef-bbef7101cc61/Picture2.png" alt=""><figcaption><p>Using “MFTECmd” to parse the “$J” data stream</p></figcaption></figure>



We used the “--csv” switch to get the parsing results in CSV format so it can be further inspected and analyzed with software made for that purpose. [Timeline Explorer.exe](https://ericzimmerman.github.io/#!index.md) is a good choice for our purposes and is highly recommended for forensic investigators.

<figure><img src="https://images.squarespace-cdn.com/content/v1/60d08f10063a3d3fb6875391/e0112889-00ab-4148-a914-808ecd789708/Picture3.png" alt="" height="185" width="535"><figcaption><p>The parsed “$J” data stream viewed in “Timeline Explorer”</p></figcaption></figure>



Note that Parent Path has no values, because the “$J” records don’t store such information, such information can be either correlated manually by going through the Master File Table ($MFT) and matching the entry numbers in both records, or “$MFT” can be passed to “MFTECmd” tool as an argument and automatic correlation will be conducted by the tool itself.

<figure><img src="https://images.squarespace-cdn.com/content/v1/60d08f10063a3d3fb6875391/057a85ac-d963-45f6-8acd-583970f04e71/Picture4.png" alt="" height="269" width="491"><figcaption><p>Parsing the “$J” data stream and enriching it with parsed “$MFT” information to show the full path</p></figcaption></figure>

<figure><img src="https://images.squarespace-cdn.com/content/v1/60d08f10063a3d3fb6875391/c345c57d-e777-4b8c-b54b-4b44598963dd/Picture5.png" alt="" height="149" width="518"><figcaption><p>The parsed and merger of “USN Journal” and “Master File Table” records viewed in “Timeline Explorer”</p></figcaption></figure>



## Detection Techniques

* [https://blog.haboob.sa/blog/advanced-usn-journal-forensics](https://blog.haboob.sa/blog/advanced-usn-journal-forensics)







***

## REFERENCES

* [https://blog.haboob.sa/blog/advanced-usn-journal-forensics](https://blog.haboob.sa/blog/advanced-usn-journal-forensics)
* [https://binaryforay.blogspot.com/2018/06/introducing-mftecmd.html](https://binaryforay.blogspot.com/2018/06/introducing-mftecmd.html)

