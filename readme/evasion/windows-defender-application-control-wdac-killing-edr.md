---
description: 'MITRE ATT&CK™ Impair Defenses: Disable or Modify Tools - Technique T1562.001'
icon: windows
---

# Windows Defender Application Control (WDAC): Killing EDR

Theory

Windows Defender Application Control (WDAC) was introduced with Windows 10 and allows organizations to control which drivers and applications are allowed to run on their Windows clients. It was designed as a security feature under the [servicing criteria](https://www.microsoft.com/msrc/windows-security-servicing-criteria), defined by the Microsoft Security Response Center (MSRC).

**EDR drivers or binaries can therefore be blocked using a WDAC policy.**

In order to bypass EDR products using the following method, a reboot is required, which is a bad OPSEC operation.

### Practice <a href="#practice" id="practice"></a>

{% hint style="success" %}
In order to set up a Windows Defender Application Control (WDAC) policy that can tamper with a targeted EDR, follow this guide:
{% endhint %}



## Locally

#### 1. Setup Your Environement <a href="#id-1.-setup-your-environement" id="id-1.-setup-your-environement"></a>

On a fresh installed Windows Virtual machine, we will install:

* [Dotnet 8 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/sdk-8.0.403-windows-x64-installer)
* [WDAC Wizzard](https://webapp-wdac-wizard.azurewebsites.net/)
* The targetted EDR Agent

#### 2. Create a WDAC Policy <a href="#id-2.-create-a-wdac-policy" id="id-2.-create-a-wdac-policy"></a>

When all setup, we can start creating an EDR-Blocking WDAC Policy using the WDAC Wizzard utility:

1. Select "Policy Editor"

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252FpgulpaVarQIy0lA4idjN%252Fimage-20241009110409414.png%3Falt%3Dmedia%26token%3Db5a05316-0eb3-4af2-9290-408363c9358a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=688cf5db&#x26;sv=2" alt=""><figcaption></figcaption></figure>

1. Select the "AllowAll" template from `C:\Windows\Schemas\CodeIntgrity\ExamplePolicies\AllowAll.xml` and click "Next"

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252F3C1qVlckYQW0y4G1rlyV%252Fimage-20241009110346223.png%3Falt%3Dmedia%26token%3Dc87b2bdc-3ae5-4ff6-8b72-6a441a2018f1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=808d4857&#x26;sv=2" alt=""><figcaption></figcaption></figure>

1. Ensure that "Audit Mode" is Unchecked, click "Next"

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252FXvPvoOsRrWSiEz6qtLUY%252Fimage-20241008151153062.png%3Falt%3Dmedia%26token%3Db977fb6f-022d-40ab-a7e0-4dc761803842&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=250e93e7&#x26;sv=2" alt=""><figcaption></figcaption></figure>

1. Click "Add Custom"

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252FpOVtNDwzvod8XX1OOFCg%252Fimage-20241009111120016.png%3Falt%3Dmedia%26token%3Df5d200f0-8f18-46f2-9c96-9fe96c64967e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b08aebb0&#x26;sv=2" alt=""><figcaption></figcaption></figure>

1. Specify conditions on the targeted EDR Publisher, executable/drivers hashes, Product Name, or even Paths.

For this technique to be effective in tampering with EDR functions, it is essential to identify and select both user-land processes (e.g., PE/exe files) and drivers (e.g., sys files) that are necessary for the EDR's to properly work.

However, avoid blocking entire EDR related drivers and processes, as this may lead to system crashes or blue screens. Instead, **focus on blocking the minimal components, necessary to interfere with the essential functions of the EDR.**

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252FcFKI3wklAaLX1LdytLy8%252Fimage-20241008161041864.jpg%3Falt%3Dmedia%26token%3D35ce9cf1-ba36-420d-8c1f-a382b199433f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5f1c54d0&#x26;sv=2" alt=""><figcaption></figcaption></figure>

1. When done, wait for the WDAC Policy to build. It will create an XML and PolicyBinary file.

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252F4krJ0scpEMC7JwtJTZzA%252Fimage.png%3Falt%3Dmedia%26token%3Db0420c1f-e4bd-4986-b2ab-06ec0b33cef1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=8d47cb4b&#x26;sv=2" alt=""><figcaption></figcaption></figure>

#### 3. Apply the WDAC Policy <a href="#id-3.-apply-the-wdac-policy" id="id-3.-apply-the-wdac-policy"></a>

We can now upload the previously build PolicyBinary file to a target host, and [apply it](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/deployment/appcontrol-deployment-guide) using below command lines:

Copy

```powershell
# Windows 11 22H2 and above
CiTool --update-policy C:\Path\To\{Policy}.cip

# Windows 11, Windows 10 version 1903 and above, 
# And Windows Server 2022 and above
$PolicyBinary = "C:\Path\To\{Policy}.cip"
$DestinationFolder = $env:windir+"\System32\CodeIntegrity\CIPolicies\Active\"
$RefreshPolicyTool = "<Path where RefreshPolicy.exe can be found from managed endpoints>"
Copy-Item -Path $PolicyBinary -Destination $DestinationFolder -Force
& $RefreshPolicyTool

# All other versions of Windows and Windows Server
$PolicyBinary = "C:\Path\To\{Policy}.cip"
$DestinationBinary = $env:windir+"\System32\CodeIntegrity\SiPolicy.p7b"
Copy-Item  -Path $PolicyBinary -Destination $DestinationBinary -Force
Invoke-CimMethod -Namespace root\Microsoft\Windows\CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{FilePath = $DestinationBinary}
```

<figure><img src="https://red.infiltr8.io/~gitbook/image?url=https%3A%2F%2F329872044-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FMdUKdzuqIuObdvCB3mUR%252Fuploads%252FFnkzYewrqtZPRvb73z6x%252Fimage-20241008161514514.png%3Falt%3Dmedia%26token%3Dbbbf9201-901a-49a1-9648-e7696b4f7278&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e8f31523&#x26;sv=2" alt=""><figcaption></figcaption></figure>

#### 4. Reboot <a href="#id-4.-reboot" id="id-4.-reboot"></a>

After reboot, (and maybe several tests to identify which process/driver to block) the EDR should be now disabled.



***

## REFERENCES

* [https://red.infiltr8.io/redteam/evasion/endpoint-detection-respons-edr-bypass/windows-defender-application-control-wdac-killing-edr](https://red.infiltr8.io/redteam/evasion/endpoint-detection-respons-edr-bypass/windows-defender-application-control-wdac-killing-edr)
* [https://beierle.win/2024-12-20-Weaponizing-WDAC-Killing-the-Dreams-of-EDR/#local-machine](https://beierle.win/2024-12-20-Weaponizing-WDAC-Killing-the-Dreams-of-EDR/#local-machine)
