# OWASP-ZSC

{% embed url="https://github.com/OWASP/ZSC" %}



## Help Menu

```
zsc> help
```

## Generate Shellcode

```
zsc> shellcode

zsc> generate
```

{% hint style="info" %}
You can use tab compilation&#x20;
{% endhint %}



## Generate Linux Shellcode

```
zsc/shellcode/generate/> linux_x86
```

### Generate system("/bin/sh") payload with no encoders

```
zsc/shellcode/generate/linux_x86> system
```

```
zsc/shellcode/generate/linux_x86/system> command_to_execute
```

```
command_to_execute> /bin/sh
```

```
zsc/shellcode/generate/linux_x86/system/encode_type> 
```

```
zsc/shellcode/generate/linux_x86/system/encode_type> none
```

```
Output assembly code?(y or n)> y
```

```
Output shellcode to screen?(y or n)> y
```

```
Shellcode output to a .c file?(y or n)> n
```



### Generate system("/bin/sh") with xor\_random encoder

```
python3 zsc.py -p linux_x86/system/xor_random -i /bin/sh
```



{% hint style="info" %}
Now, Copy the shellcode and paste into the PoC
{% endhint %}



## Search for Shell\_Storm Shell Code

```
python3 zsc.py --shell-storm search 'linux/x86 bind 1337'
```

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

### Download the shellcode

```
python3 zsc.py --shell-storm download 882
```



## Obsfucate the Exploit

```
zsc> help
```

```
zsc> obfuscate
```

```
zsc/obfuscate> python
```

```
filename> /home/l3mon/Desktop/hello.py
```

```
encode> simple_base64_rev
```

{% hint style="info" %}
The original code will be at the top within comments.

Followed by the obfuscated code.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
