# 📄 API Documentation

## API Documentation

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-api-documentation/api-testing/api-documentation" %}

Documentation can be in both human-readable and machine-readable forms. Human-readable documentation is designed for developers to understand how to use the API. It may include detailed explanations, examples, and usage scenarios.

Machine-readable documentation is designed to be processed by software for automating tasks like API integration and validation. It's written in structured formats like JSON or XML.

API documentation is often publicly available, particularly if the API is intended for use by external developers. If this is the case, always start your recon by reviewing the documentation.



***

## Discovering API Documentation

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-api-documentation/api-testing/discovering-api-documentation" %}

Look for endpoints that may refer to API documentation, for example:

```
/api
/swagger/index.html
/openapi.json
```

If you identify an endpoint for a resource, make sure to investigate the base path. For example, if you identify the resource endpoint `/api/swagger/v1/users/123`, then you should investigate the following paths:

* `/api/swagger/v1`
* `/api/swagger`
* `/api`



***

## Using Machine Readable Documentation



{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-api-documentation/api-testing/using-machine-readable-documentation" %}

You can use a range of automated tools to analyze any machine-readable API documentation that you find.

You can use Burp Scanner to crawl and audit OpenAPI documentation, or any other documentation in JSON or YAML format. You can also parse OpenAPI documentation using the OpenAPI Parser BApp.

You may also be able to use a specialized tool to test the documented endpoints, such as Postman or SoapUI.
