# Task 1: Gather Information About a Target Website using Ping Command Line Utility

```
ping www.certifiedhacker.com
```

```
ping www.certifiedhacker.com -f -l 1500
```

\-f: specifies setting not fragmenting flag in packet

\-l: Specifies buffer size

```
ping www.certifiedhacker.com -i 3
```

\-i: sets the time to live value (MAX=255)

```
ping www.certifiedhacker.com -i 2 -n 1
```

\-n: specifies the number of echo requests  to be sent to the target



Use the ping command-line utility to test the reachability of the website www.eccouncil.org. Identify the maximum packet/frame size on this machine’s network.&#x20;

1472

