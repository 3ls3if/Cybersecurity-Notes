---
icon: chrome
---

# Fuzzing Chrome V8 Engine

## Introduction to [Fuzzilli](https://github.com/googleprojectzero/fuzzilli)

A (coverage-)guided fuzzer for dynamic language interpreters based on a custom intermediate language ("FuzzIL") which can be mutated and translated to JavaScript.

## Usage

1. Download the source code for one of the supported JavaScript engines. See the [Targets/](https://github.com/googleprojectzero/fuzzilli/blob/main/Targets) directory for the list of supported JavaScript engines.
2. Apply the corresponding patches from the target's directory. Also see the README.md in that directory.
3. Compile the engine with coverage instrumentation (requires clang >= 4.0) as described in the README.
4. Compile the fuzzer: `swift build [-c release]`.
5. Run the fuzzer: `swift run [-c release] FuzzilliCli --profile=<profile> [other cli options] /path/to/jsshell`. See also `swift run FuzzilliCli --help`.

## Read More [Here](https://github.com/googleprojectzero/fuzzilli)



## Other Fuzzer

* FreeDom: [https://github.com/sslab-gatech/freedom](https://github.com/sslab-gatech/freedom)







***

## REFERENCES

* [https://apt29a.blogspot.com/2022/01/fuzzing-chromes-javascript-engine-v8.html](https://apt29a.blogspot.com/2022/01/fuzzing-chromes-javascript-engine-v8.html)
* [https://googleprojectzero.blogspot.com/2020/10/announcing-fuzzilli-research-grant.html](https://googleprojectzero.blogspot.com/2020/10/announcing-fuzzilli-research-grant.html)
* [https://edu.google.com/programs/credits/research/?modal\_active=none](https://edu.google.com/programs/credits/research/?modal\_active=none)
* [https://fuzzinglabs.com/fuzzing-javascript-wasm-dharma-chrome-v8/](https://fuzzinglabs.com/fuzzing-javascript-wasm-dharma-chrome-v8/)
* [https://www.youtube.com/watch?v=MLz86hFyGwY](https://www.youtube.com/watch?v=MLz86hFyGwY)
* [https://blog.doyensec.com/2020/09/09/fuzzilli-jerryscript.html](https://blog.doyensec.com/2020/09/09/fuzzilli-jerryscript.html)
* [https://github.com/googleprojectzero/fuzzilli](https://github.com/googleprojectzero/fuzzilli)
* [https://github.com/sslab-gatech/freedom](https://github.com/sslab-gatech/freedom)
