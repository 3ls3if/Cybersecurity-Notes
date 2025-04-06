---
icon: shield-check
---

# InvisibilityCloak - C# Obfuscation Toolkit

### InvisibilityCloak - C# Obfuscation Toolkit

**InvisibilityCloak** is a proof-of-concept obfuscation tool designed specifically for C# post-exploitation projects. Its main goal is to evade **signature-based detections** (like Microsoft Defender) by modifying key characteristics of the source code in Visual Studio projects. This includes:

* Renaming the tool and altering its project GUID
* Obfuscating compatible strings using Base64, ROT13, or string reversal
* Removing one-line comments
* Optionally removing PDB string metadata from compiled assemblies

> This tool is particularly useful for red teamers and security researchers looking to bypass static detection mechanisms in offensive C# tools.

***

### Features

* Change tool name and project GUID
* String obfuscation: `base64`, `rot13`, or `reverse`
* Compatible with both **Windows** and **Linux** (Debian-based)
* Python3-based command-line utility

***

### Usage

#### Basic Syntax

```bash
python InvisibilityCloak.py -d <project_directory> -n <new_tool_name> -m <obfuscation_method>
```

#### Options

| Argument            | Description                                         |
| ------------------- | --------------------------------------------------- |
| `-d`, `--directory` | Path to your Visual Studio C# project               |
| `-n`, `--name`      | New name for the obfuscated tool                    |
| `-m`, `--method`    | Obfuscation method: `base64`, `rot13`, or `reverse` |
| `-h`, `--help`      | Display help menu                                   |
| `--version`         | Show version info                                   |

***

#### Examples

**🔹 Base64 String Obfuscation**

```bash
python InvisibilityCloak.py -d /path/to/project -n "StealthTool" -m base64
```

**🔹 ROT13 String Obfuscation**

```bash
python InvisibilityCloak.py -d C:\path\to\project -n "StealthTool" -m rot13
```

**🔹 Reverse String Obfuscation**

```bash
python InvisibilityCloak.py -d /path/to/project -n "StealthTool" -m reverse
```

**🔹 Rename Tool Without String Obfuscation**

```bash
python InvisibilityCloak.py -d C:\path\to\project -n "StealthTool"
```

***

## REFERENCES

* [https://github.com/matterpreter/DefenderCheck](https://github.com/matterpreter/DefenderCheck)
* [https://github.com/h4wkst3r/InvisibilityCloak](https://github.com/h4wkst3r/InvisibilityCloak)



