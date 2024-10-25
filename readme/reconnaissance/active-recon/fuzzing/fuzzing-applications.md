---
description: Fuzzing binaries in modern times!
icon: file-binary
---

# Fuzzing Applications

## Introduction

Fuzz testing or fuzzing is a software testing technique, and it is a type of Security Testing. Fuzz Testing is a type of testing intended to discover coding errors and security loopholes in software, operating systems, or networks. This involves monitoring the target system by inputting invalid or random data called FUZZ to the system. where automated or semi-automated testing techniques are used.

<figure><img src="../../../../.gitbook/assets/image (231).png" alt=""><figcaption><p>Source: <a href="https://www.guru99.com/fuzz-testing.html">https://www.guru99.com/fuzz-testing.html</a></p></figcaption></figure>

## Fuzz Testing Steps

The steps for fuzzy testing include the basic testing steps-

* **Step 1)** Identify the target system
* **Step 2)** Identify inputs
* **Step 3)** Generate Fuzzed data
* **Step 4)** Execute the test using fuzzy data
* **Step 5)** Monitor system behavior
* **Step 6)** Log defects

## Existing Fuzzing Types

* Open Source
* Closed Source
* Network Protocol Fuzzing
* Parser Fuzzing
* Grammar-based Fuzzing
* Snapshot Fuzzing
* (Linux) Kernel Fuzzing
* Smart Contract Fuzzing

## Tools&#x20;

* AFL++
* Fuzzilli
* Jackalope
* Syzkaller
* Python3

## Writing a Fuzzer

* Sending random inputs to a target program.
* Creating a mutation engine.
* Monitor target state.
* Record crash and save interesting input cases.

## Code Coverage Fuzzing with AFL++

### Vim [CVE-2019-20079](https://nvd.nist.gov/vuln/detail/CVE-2019-20079)&#x20;

Downloading the vulnerable version of Vim:

```
[+] Git clone VIM
cmd$ git clone https://github.com/vim/vim.git ; cd vim

[+] Compile and Make VIM with AFL++ 
cmd$ CC=afl-clang-fast CXX=afl-clang-fast++ ./configure --with-features=huge --enable-gui=none
cmd$ make -j4 ; cd src/

[+] Feed Corpus
cmd$ mkdir corpus ; mkdir output 
cmd$ echo "a*b\+\|[0-9]\|\d{1,9}" > corpus/1 ; echo "^\d{1,10}$" > corpus/2

[+] Fuzzing VIM
cmd$ afl-fuzz -m none -i corpus -o output ./vim -u NONE -X -Z -e -s -S @@ -c ':qa!'
```

The above options used -u NONE and -X is to speed up vim startup. Options -e -s are used to make vim silent and to avoid 'MORE' prompt which could block VIM, the option -Z disables the external commands which makes fuzzing safer. I've also created a small bash script which automates the above tasks for you \[[vimfuzz.sh](https://github.com/RootUp/fuzzingvim)].\
\
While fuzzing, fuzz it on ram file system to avoid making too much I/O something like:  _sudo mount -t tmpfs -o size=6g tmpfs /home/afl-fuzz-user/afl-fuzz._ Aside you can use \[[pack.sh](https://github.com/RootUp/PersonalStuff/blob/master/pack.sh)] a script which contains some standard ubuntu packages so you dont get much dependence issues while compiling any target. Keep fuzzing :)



***

## REFERENCES

* [https://www.qatouch.com/blog/introduction-to-fuzz-testing/](https://www.qatouch.com/blog/introduction-to-fuzz-testing/)
* [https://www.guru99.com/fuzz-testing.html](https://www.guru99.com/fuzz-testing.html)
* [https://blog.isosceles.com/how-to-build-a-corpus-for-fuzzing/](https://blog.isosceles.com/how-to-build-a-corpus-for-fuzzing/)
* [https://github.com/20urc3/Aplos](https://github.com/20urc3/Aplos)
* [https://bushido-sec.com/index.php/2023/06/19/the-art-of-fuzzing/](https://bushido-sec.com/index.php/2023/06/19/the-art-of-fuzzing/)
* [https://www.inputzero.io/2020/03/fuzzing-vim.html](https://www.inputzero.io/2020/03/fuzzing-vim.html)
