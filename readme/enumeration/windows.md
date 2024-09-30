# 🪟 Windows

## Searching Commands

### dir

```
# help
dir /?

# search for all .txt files
dir *.txt /s

# pause when the screen is full
dir *.txt /s /b

# list directories only
dir /a:d

# list contents except directories
dir /a:-d

# display hidden directories
dir /a:h
```

### find

```
# help 
find /?

# Search for words in a file
find "hello" story.txt

# Ignore the character case
find /i "Hello" story.txt

# Count number of empty strings
type story.txt | find " " /v /c
```

## WinPEAS

{% embed url="https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS" %}

{% embed url="https://lnkd.in/gKRkqd6n" %}
