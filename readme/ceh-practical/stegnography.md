# 🖊 Stegnography

## Tools

* Snow: For hiding and extracting hidden data from a text file.
* Openstego: For hiding and extracting hidden data from an image file
* Covert TCP: For hiding data in TCP/IP packet headers

## Snow Tool

### Hide a message

```
snow.exe -C -m "Hidden message" -p "password" Secret.txt <outputfile.txt>
```

### Extract a message

```
snow.exe -C -p "password" <Filename.txt>
```



## Openstego Tool

### Hide Data

* Click Hide Data
* Select a file
* Select a cover file
* Give a output file name
* Click on Hide Data button

### Extract Data

* Click on Extract Data
* Select the image
* Select the output file
* Click on Extract Data

## Covert TCP

Covert TCP help us to hide the data that is being sent over the network by manipulating the TCP/IP header.

We send the data in the left out spaces present in the header 1 Byte at a time.

### Sender Machine

```
./covert_tcp -source <ip address of sender> -dest <ip address of receiver> -source_port <origin port number> -dest <reciever port number> -file <file name> 
```

### Receiver Machine

```
./covert_tcp -source <ip address of sender> -source_port <sender destination port number> -server -file <file name>
```
