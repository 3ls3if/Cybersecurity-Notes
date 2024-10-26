---
icon: user-ninja
---

# Detecting Hidden Processes

## Introduction to WinDbg

WinDbg is a kernel-mode and user-mode debugger that's included in Debugging Tools for Windows.

For information about how to get Debugging Tools for Windows, see [Download and install the WinDbg Windows debugger](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/). After you have installed the debugging tools, locate the installation directories for 64-bit (x64) and 32-bit (x86) versions of the tools. For example:

* **C:\Program Files (x86)\Windows Kits\10\Debuggers\x64**
* **C:\Program Files (x86)\Windows Kits\10\Debuggers\x86**



## Step By Step Guide

* **Attach WinDbg to the Target System**: Open WinDbg as an administrator and attach it to the target system or dump file.
* **Set Context to Kernel Mode**:

```
.symfix
.reload
```

* **List All Active Processes**: Use the `!process 0 0` command to list all processes. This lists active processes maintained by the `PsActiveProcessHead` list.

```
!process 0 0
```

* **Manually Search for Process Objects**: Hidden processes may still have allocated `EPROCESS` structures. Search the kernel memory for process objects using:

```
!object \
```

## Useful Commands

| vercommand | Show Debugger Command Line                               |
| ---------- | -------------------------------------------------------- |
| vertarget  | Show Target Computer Version                             |
| !cpuid     | Displays information about the processors on the system  |
| .sympath   | Set Symbol Path                                          |
| !lmi       | Displays detailed information about a module             |
| \|         | Process Status                                           |
| \~         | Thread Status                                            |
| lm         | List Loaded Modules                                      |
| ?          | Evaluate Expression                                      |
| x          | Examine Symbols                                          |
| bp         | Set Breakpoint                                           |
| bl         | Breakpoint Enable                                        |
| g          | Go                                                       |
| r          | Registers                                                |
| dp         | Display Memory - Pointer-sized values                    |
| dps        | Display Referenced Memory - Display known symbols        |
| k          | Display Stack Backtrace                                  |
| ln         | List Nearest Symbols                                     |
| da         | Display Memory - ASCII characters                        |
| dc         | Display Memory - Double-word values and ASCII characters |
| dt         | Display Type                                             |
| dS         | Display String - UNICODE\_STRING structure               |
| du         | Display Memory - Wide char characters                    |
| db         | Display Memory - ASCII characters                        |
| dw         | Display Memory - Word values                             |
| dd         | Display Memory - Double-word values                      |
| dq         | Display Memory - Quad-word values                        |
| u          | Unassemble                                               |
| ub         | Unassemble backward                                      |
| uf         | Unassemble Function                                      |





***

## REFERENCES

* [https://www.youtube.com/watch?v=pKQ\_Io\_8lTc](https://www.youtube.com/watch?v=pKQ\_Io\_8lTc)
* [https://www.youtube.com/watch?v=usW9F\_bUpvQ\&t=826s\&ab\_channel=OffByOneSecurity](https://www.youtube.com/watch?v=usW9F\_bUpvQ\&t=826s\&ab\_channel=OffByOneSecurity)
* [https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/getting-started-with-windbg--kernel-mode-](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/getting-started-with-windbg--kernel-mode-)
* [https://codemachine.com/articles/windbg\_quickstart.html](https://codemachine.com/articles/windbg\_quickstart.html)
