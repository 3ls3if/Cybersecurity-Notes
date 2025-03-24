---
icon: shield
---

# Detection of Windows Defender Tampering via Powershell

{% hint style="success" %}
ID: T1562.001Sub-technique of:  [T1562](https://attack.mitre.org/techniques/T1562)
{% endhint %}

## Impair Defenses: Disable or Modify Tools (T1562.001)

**Overview**

The technique "Disable or Modify Tools" (T1562.001) under the broader category of "Impair Defenses" involves adversaries taking actions to disable or modify security tools and software on a target system. This can include antivirus software, endpoint detection and response (EDR) tools, firewalls, and other defensive mechanisms. By disabling or modifying these tools, adversaries can evade detection, prevent logging of their activities, and gain persistent access to the system.

**Common Methods**

1. <mark style="color:green;">**Service Disabling**</mark><mark style="color:green;">: Adversaries may stop or disable services associated with security tools. This can be done using commands like</mark> <mark style="color:green;"></mark><mark style="color:green;">`sc stop`</mark> <mark style="color:green;"></mark><mark style="color:green;">or</mark> <mark style="color:green;"></mark><mark style="color:green;">`net stop`</mark> <mark style="color:green;"></mark><mark style="color:green;">in Windows, or by modifying service configurations.</mark>
   * <mark style="color:green;">**Example**</mark><mark style="color:green;">:</mark> <mark style="color:green;"></mark><mark style="color:green;">`sc stop WinDefend`</mark>
2. <mark style="color:green;">**Registry Modifications**</mark><mark style="color:green;">: Changing registry keys can disable security software. For instance, modifying registry entries related to Windows Defender or other antivirus programs.</mark>
   * <mark style="color:green;">**Example**</mark><mark style="color:green;">: Modifying the</mark> <mark style="color:green;"></mark><mark style="color:green;">`DisableAntiSpyware`</mark> <mark style="color:green;"></mark><mark style="color:green;">registry key to disable Windows Defender.</mark>
3. <mark style="color:green;">**File Deletion or Modification**</mark><mark style="color:green;">: Adversaries may delete or modify executable files, configuration files, or other components of security software to render them ineffective.</mark>
   * <mark style="color:green;">**Example**</mark><mark style="color:green;">: Deleting the</mark> <mark style="color:green;"></mark><mark style="color:green;">`MsMpEng.exe`</mark> <mark style="color:green;"></mark><mark style="color:green;">file, which is the main executable for Windows Defender.</mark>
4. <mark style="color:green;">**Group Policy Modifications**</mark><mark style="color:green;">: Changing group policies can disable security features. For example, setting policies to disable Windows Defender or other security tools.</mark>
   * <mark style="color:green;">**Example**</mark><mark style="color:green;">: Using</mark> <mark style="color:green;"></mark><mark style="color:green;">`gpedit.msc`</mark> <mark style="color:green;"></mark><mark style="color:green;">to disable Windows Defender via group policy.</mark>
5. <mark style="color:green;">**Task Scheduler Modifications**</mark><mark style="color:green;">: Adversaries may modify or delete scheduled tasks that are used to run security scans or updates.</mark>
   * <mark style="color:green;">**Example**</mark><mark style="color:green;">: Deleting a scheduled task that runs a daily antivirus scan.</mark>



***

## Checking Windows Defender Service Status

You can check the status of the Windows Defender service to ensure it is running properly.

```
Get-Service -Name "WinDefend"
```

#### Verifying Windows Defender Settings

You can use PowerShell to check the current settings of Windows Defender to ensure they have not been altered.

```
Get-MpPreference
```

#### Checking Windows Defender Signature Updates

Ensure that Windows Defender has the latest signature updates.

```
Get-MpComputerStatus | Select-Object AMServiceVersion, AntispywareSignatureVersion, AntivirusSignatureVersion
```

#### Checking Windows Defender Real-Time Protection Status

Verify that real-time protection is enabled.

```
Get-MpComputerStatus | Select-Object RealTimeProtectionEnabled
```

#### Checking Windows Defender Event Logs

Review the Windows Defender event logs for any suspicious activities.

```
Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational" | Where-Object { $_.Id -eq 5007 } | Format-Table -AutoSize
```

#### Checking Windows Defender Exclusions

List any exclusions that have been set in Windows Defender, which could indicate tampering.

```
Get-MpPreference | Select-Object -ExpandProperty ExclusionPathItems
```

#### Checking Windows Defender Scheduled Scans

Verify the scheduled scan settings to ensure they have not been altered.

```
Get-MpPreference | Select-Object -Property ScanPurpose, ScanScheduleQuickScanTime, ScanScheduleFullScanTime
```

#### Checking Windows Defender Cloud Protection

Ensure that cloud protection is enabled.

```
Get-MpPreference | Select-Object MAPSReportingAdvancedLevel, SubmitSamplesConsent
```





***

## REFERENCES

* [https://attack.mitre.org/techniques/T1562/001/](https://attack.mitre.org/techniques/T1562/001/)



