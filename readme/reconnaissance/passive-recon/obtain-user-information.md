# 👨‍💼 Obtain User Information

## Gather Names and Email Addresses

### [theHarvester](https://github.com/laramies/theHarvester)

```
theharvester -d <target domain> -b google
```

* \-d : This identifies the domain to be searched; usually the domain or target's website.
* \-b : This identifies the source for extracting the data; it must be one of the following: Bing, BingAPI, Google, Google-Profiles, Jigsaw, LinkedIn, People123, PGP, or All
* \-l : This limit option instructs theharvester to only harvest data from a specified number of returned search results.
* \-f : This option is used to save the final results to an HTML and an XML file. If this option is omitted, the results will be displayed on the screen and not saved.

***

## Gather Document Metadata

### [Metagoofil](https://github.com/opsdisk/metagoofil)

```
metagoofil -d microsoft.com -t doc -l 25 -o microsoft -f microsoft.html
```



***

## Profile Users for Password List

### [Common User Password Profiler (CUPP)](https://github.com/Mebus/cupp)

```
# Download and Install
git clone https://github.com/Mebus/cupp.git

# Run in interactive mode
python cupp.py -i
```



***

