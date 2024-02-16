# 🚧 Testing for server-side parameter pollution in structured data formats

An attacker may be able to manipulate parameters to exploit vulnerabilities in the server's processing of other structured data formats, such as a JSON or XML. To test for this, inject unexpected structured data into user inputs and see how the server responds.

Consider an application that enables users to edit their profile, then applies their changes with a request to a server-side API. When you edit your name, your browser makes the following request:

```
POST /myaccount
name=peter
```

This results in the following server-side request:

```
PATCH /users/7312/update
{"name":"peter"}
```

You can attempt to add the `access_level` parameter to the request as follows:

```
POST /myaccount
name=peter","access_level":"administrator
```

If the user input is added to the server-side JSON data without adequate validation or sanitization, this results in the following server-side request:

```
PATCH /users/7312/update
{name="peter","access_level":"administrator"}
```

This may result in the user `peter` being given administrator access.

{% hint style="info" %}
**Related pages**

For information on how to identify parameters that you can inject into the query string, see the Finding hidden parameters section.
{% endhint %}

Consider a similar example, but where the client-side user input is in JSON data. When you edit your name, your browser makes the following request:

```
POST /myaccount
{"name": "peter"}
```

This results in the following server-side request:

```
PATCH /users/7312/update
{"name":"peter"}
```

You can attempt to add the `access_level` parameter to the request as follows:

```
POST /myaccount
{"name": "peter\",\"access_level\":\"administrator"}
```

If the user input is decoded, then added to the server-side JSON data without adequate encoding, this results in the following server-side request:

```
PATCH /users/7312/update
{"name":"peter","access_level":"administrator"}
```

Again, this may result in the user `peter` being given administrator access.

Structured format injection can also occur in responses. For example, this can occur if user input is stored securely in a database, then embedded into a JSON response from a back-end API without adequate encoding. You can usually detect and exploit structured format injection in responses in the same way you can in requests.

{% hint style="info" %}
**Note**

This example below is in JSON, but server-side parameter pollution can occur in any structured data format. For an example in XML, see the XInclude attacks section in the XML external entity (XXE) injection topic.
{% endhint %}

