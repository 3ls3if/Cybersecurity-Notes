# Password Cracking using Rules

## Introduction

A rule file defines a set of transformations to apply to dictionary words to create password candidates during brute-force or dictionary attacks. Each line in a rule file specifies one or more operations, like appending characters, substituting letters, reversing words, etc. Rule files allow for efficient generation of password candidates without having to manually create variations of each word.

## Why Use Rule Files?

* **Efficiency**: Rules allow you to create password variations quickly without exponentially increasing the size of your wordlist.
* **Targeted Attacks**: They can help you customize attacks to fit patterns observed in real-world passwords, focusing on common tweaks users make, like adding numbers or special characters.
* **Resource Management**: By avoiding overly large dictionaries, rule-based cracking can be faster and less resource-intensive.

## Tools

* **Hashcat**: A widely-used GPU-based password cracker that supports complex rule files with a variety of transformations.
* **John the Ripper**: Another powerful tool that uses a simple syntax for rules in its `.rules` files. It's commonly used for CPU-based cracking.

## Rule File Syntax

```
# Character Manipulation:
    l: Convert to lowercase.
    u: Convert to uppercase.
    c: Capitalize the first letter.
    t: Toggle case of each character.
    
# Appending & Prepending:
    $X: Append character X.
    ^X: Prepend character X.
    
# Substitutions:
    sXY: Substitute character X with Y.
    Example: sa@ replaces all instances of "a" with "@".
    
# Reversing & Duplication:
    r: Reverse the word.
    d: Duplicate the word (e.g., "passpass").
```

## Hashcat Commands

{% hint style="info" %}
Use the `--rules` option to specify a rule file, often located in the `/rules/` directory of Hashcat.
{% endhint %}

```
hashcat -a 0 -m 1000 hash.txt wordlist.txt -r rules/best64.rule
```

## John the Ripper Commands

{% hint style="info" %}
Specify rules within the configuration file (`john.conf`) or use predefined rules.
{% endhint %}

```
john --wordlist=wordlist.txt --rules --format=NT hash.txt
```

## Custom Rule File

```
^p       // Prepend 'p' to each word
$123     // Append '123' to each word
sa@      // Replace 'a' with '@'
```

## Common Rule Files

* **Best64.rule**: A popular rule file with basic transformations, often used for quick attacks.
* **OneRuleToRuleThemAll**: A large rule file designed to cover a wide array of transformations.
* **Leetspeak.rule**: Transforms characters into "leet" equivalents (e.g., replacing "E" with "3").

## Password Cracking Case Study

### Quick Wins

If we're in need of cracking any account password quickly, we can use rockyou.txt with a ruleset like OneRule ([https://lnkd.in/gQsYHC5y](https://lnkd.in/gQsYHC5y)). This should take a few minutes to run.

```
hashcat.exe -m 1000 hashes.txt rockyou.txt -r OneRuleToRuleThemAll.rule -O
```

### Medium Runs

You can use a larger wordlist, such as rockyou2021.txt with a ruleset. This will crack more hashes, but take more time. This takes around 1.5 hours for me to run. Between step 1 and 2, you'll likely find 70% of your hashes

```
hashcat.exe -m 1000 hashes.txt Downloads\rockyou2021.txt -r OneRuleToRuleThemAll.rule -O
```

### Diving Deeper

There are all sorts of strategies you can use to find hashes that do not crack in steps 1 or 2\
\
One thing that works incredibly well is building a custom wordlist based on known cracked passwords (you can go as far as just including your entire pot file), computer names, usernames, nearby sports teams, and words unique to the company (you can crawl the website with a tool like CeWL or even use ChatGPT)\
\
Once you have your wordlist, you can use a large ruleset (such as [https://lnkd.in/g5Vypy46](https://lnkd.in/g5Vypy46)) against it. You can also try using various larger rulesets to see if you get different results. This should only take a few seconds with a smaller wordlist

```
hashcat.exe -m 1000 hashes.txt customwordlist.txt -r rules_full.rule -O
```

If you get new cracked hashes, simply add them into your wordlist and run it again. Rinse and repeat until you get no more cracks

Once this path is exhausted, you can shift to mask attacks ([https://lnkd.in/gT6vsmWb](https://lnkd.in/gT6vsmWb)). If the password policy is 8 characters, you could do the following to brute force all known 8 character passwords:

```
hashcat.exe -a 3 -m 1000 hashes.txt ?a?a?a?a?a?a?a?a -O
```

This takes around 14 hours, so it's an overnight job. Quicker wins could look be looking for common traits, such as a capital letter, six any characters, and a special character at the end. This would only take around an hour, but would also be accomplished by the original brute force listed above

```
hashcat.exe -a 3 -m 1000 hashes.txt ?u?a?a?a?a?a?a?s -O
```

An even better strategy is to review common words used in already cracked passwords. Let's say they're using 'Welcome' quite a bit, followed by four random numbers and a special character

```
hashcat.exe -a 3 -m 1000 hashes.txt Welcome?d?d?d?d?s -O
```

Get creative. Once you've exhausted all mask attacks, feed these back into your custom wordlist and run it with the big ruleset

### Other Considerations

Consider making wordlists around current events. There's an election ongoing and we're cracking a ton of election-themed passwords





## REFERENCES

* [https://github.com/NotSoSecure/password\_cracking\_rules/blob/master/OneRuleToRuleThemAll.rule](https://github.com/NotSoSecure/password\_cracking\_rules/blob/master/OneRuleToRuleThemAll.rule)
* [https://www.linkedin.com/search/results/all/?fetchDeterministicClustersOnly=true\&heroEntityKey=urn%3Ali%3Afsd\_profile%3AACoAAAbq35MBEtMZgFHYQhDJ8lKVSkS3UUJuOc0\&keywords=heath%20adams\&origin=RICH\_QUERY\_SUGGESTION\&position=0\&searchId=46bcdbd4-6a86-424e-a934-f045d221b893\&sid=G39\&spellCorrectionEnabled=false](https://www.linkedin.com/search/results/all/?fetchDeterministicClustersOnly=true\&heroEntityKey=urn%3Ali%3Afsd\_profile%3AACoAAAbq35MBEtMZgFHYQhDJ8lKVSkS3UUJuOc0\&keywords=heath%20adams\&origin=RICH\_QUERY\_SUGGESTION\&position=0\&searchId=46bcdbd4-6a86-424e-a934-f045d221b893\&sid=G39\&spellCorrectionEnabled=false)
