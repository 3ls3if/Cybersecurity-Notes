---
icon: skull
---

# Reverse Engineer an API using MITMWEB and POSTMAN

## Reverse Engineer an API using MITMWEB and POSTMAN and create a Swagger file (crAPI)

Many times when we try to Pentest an API we might not get access to the Swagger file or the documentation of the API, Today we will try to create a swagger file using Mitmweb and Postman.



First we will run mitmweb through our command line in Kali

**# mitmweb**

<figure><img src="https://miro.medium.com/v2/resize:fit:786/1*qqhCZYlblmH5yApKK1jGOw.png" alt="" height="171" width="629"><figcaption><p>Running MITMWEB</p></figcaption></figure>

and as we can see it starts to listen on the port 8080 for http/https traffic, and we will make sure that it's running by navigating to the above address which is the localhost at port 8081 and we will be greeted with something like this:

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*mY6Eevp3mDoJd1RfkjccLQ.png" alt="" height="211" width="700"><figcaption><p>MITMproxy is running</p></figcaption></figure>

and then we will proxy our traffic through Burp Suite proxy port 8080 because we already has mitmweb listening for this port (make sure Burp is closed)

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*vgHc9hb_17EYTact1eLgAw.png" alt="" height="247" width="700"><figcaption><p>making the proxy port ready in the browser</p></figcaption></figure>

after this we will navigate crAPI and perform various actions like registering a user, login to the web site, forgetting password, going through different tabs, etc.

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*3cv9hrTuCWwzwuUQDjDx4Q.png" alt="" height="421" width="700"><figcaption><p>Navigating crAPI</p></figcaption></figure>

and we can see that mitmweb is capturing the traffic

<figure><img src="https://miro.medium.com/v2/resize:fit:814/1*oBbx9GRsaK9MLezWzGm7HA.png" alt="" height="427" width="651"><figcaption><p>MITMWEB is getting requests and capturing traffic</p></figcaption></figure>

and then we will check the 8081 port on the web server and find it filled with data

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*PjlcBOpXPwH231xT8hFoQw.png" alt="" height="591" width="700"><figcaption><p>Getting Flows through mitmweb</p></figcaption></figure>

then from File tab we will save the traffic flow that we captured

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*8SkBEB3c0-UgZN1z1SDuCw.png" alt="" height="627" width="700"><figcaption><p>Saving the traffic captured</p></figcaption></figure>

and then we will stop the capture and use mitmproxy2swagger to analyse it

`# sudo mitmproxy2swagger -i ./Downloads/flows -o spec.yml -p` [`http://localhost:8888/`](http://localhost:8888/) `-f flow`

what we did here is that we used the flow file for making the swagger and then limited the results from the flow file to only be for crAPI.

<figure><img src="https://miro.medium.com/v2/resize:fit:806/1*ZkP6oiDQq-B59lipzo1BLA.png" alt="" height="129" width="645"><figcaption><p>Analysing Captured file using mitmproxy2swagger</p></figcaption></figure>

after it finishes we will look at it with text editor and see what is there :

<figure><img src="https://miro.medium.com/v2/resize:fit:814/1*OWfdUByZMcIha_LGiaJJQA.png" alt="" height="519" width="651"><figcaption><p>spec.yml file after it finishes</p></figcaption></figure>

from here we will remove ignore from the files that contain APIs

<figure><img src="https://miro.medium.com/v2/resize:fit:795/1*r_frX3Gnni9paioKQMEgNQ.png" alt="" height="281" width="636"><figcaption><p>removing ignore from the APIs</p></figcaption></figure>

and we will run the previous command one more time to make a swagger file with examples:

`# sudo mitmproxy2swagger -i ./Downloads/flows -o spec.yml -p` [`http://localhost:8888/`](http://localhost:8888/) `-f flow --examples`

<figure><img src="https://miro.medium.com/v2/resize:fit:799/1*LdTikiYQC5w1GPQz9FbPqg.png" alt="" height="128" width="639"><figcaption><p>rerunning the mitmproxy2swagger</p></figcaption></figure>

from here we will go to swagger editor to visualize our file and we will upload it

[Swagger EditorEdit descriptioneditor.swagger.io](https://editor.swagger.io/?source=post_page-----99f01b58511c--------------------------------)

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*M-S5le8TAnUn51vSdEwZ8w.png" alt="" height="277" width="700"><figcaption><p>uploading our file to Editor.swagger.io</p></figcaption></figure>

and then we can analyse it and go through it more and try to get an idea about the API construction and structure.

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*CgxnTz7PbodhCzfu4SpEww.png" alt="" height="669" width="700"><figcaption><p>Analysing the API using Editor.swagger.io</p></figcaption></figure>

as we can see we make some sort of API documentation.\
from here we will go to Postman and import the .yml file to create a collection from what we did.

\# **postman**

and inside Postman we will import the yml file

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*Kg205F97_pJtHCZrUla_xA.png" alt="" height="594" width="700"><figcaption><p>Importing API file</p></figcaption></figure>

and now we can see it in the API tab and see the structure better and we can start playing with the requests from postman.

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*WCu4Ev-fM-TbXiaYRa4dvg.png" alt="" height="422" width="700"><figcaption><p>API Reverse Engineering</p></figcaption></figure>

And we can dig deeper into it

<figure><img src="https://miro.medium.com/v2/resize:fit:875/1*lOHNGnHtELWZ1DzkySPltw.png" alt="" height="332" width="700"><figcaption><p>this is the request for changing Email example</p></figcaption></figure>

As we can see mitmweb and Postman are powerful tools to see how the API is constructed and layout if you don’t have proper documentation or its a legacy API and you don’t actually know how it works and it can be useful as well for those who are doing Black Box pentesting.



***

## REFERENCES

* [https://medium.com/@amaraltohami30/reverse-engineer-an-api-using-mitmweb-and-postman-and-create-a-swagger-file-crapi-99f01b58511c](https://medium.com/@amaraltohami30/reverse-engineer-an-api-using-mitmweb-and-postman-and-create-a-swagger-file-crapi-99f01b58511c)

