# 🕵♂ API Recon

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-api-recon/api-testing/api-recon" %}

Consider the following `GET` request:

```
GET /api/books HTTP/1.1
Host: example.com
```

The API endpoint for this request is `/api/books`. This results in an interaction with the API to retrieve a list of books from a library. Another API endpoint might be, for example, `/api/books/mystery`, which would retrieve a list of mystery books.

Once you have identified the endpoints, you need to determine how to interact with them. This enables you to construct valid HTTP requests to test the API. For example, you should find out information about the following:

* The input data the API processes, including both compulsory and optional parameters.
* The types of requests the API accepts, including supported HTTP methods and media formats.
* Rate limits and authentication mechanisms.
