# 👨🎤 Identifying and Interacting with API Endpoint

## Identifying API endpoints

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-identifying-and-interacting-with-api-endpoints/api-testing/identifying-api-endpoints" %}

While browsing the application, look for patterns that suggest API endpoints in the URL structure, such as `/api/`. Also look out for JavaScript files. These can contain references to API endpoints that you haven't triggered directly via the web browser.

Burp Scanner automatically extracts some endpoints during crawls, but for a more heavyweight extraction, use the JS Link Finder BApp. You can also manually review JavaScript files in Burp.



***

## Interacting with API endpoints

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-identifying-and-interacting-with-api-endpoints/api-testing/interacting-with-api-endpoints" %}

### STEPS

* Identify API Endpoints
* Interact with them using burp repeater and intruder

{% hint style="info" %}
This enables you to observe the API's behavior and discover additional attack surface. For example, you could investigate how the API responds to changing the HTTP method and media type.
{% endhint %}

* Review the error messages

{% hint style="info" %}
As you interact with the API endpoints, review error messages and other responses closely. Sometimes these include information that you can use to construct a valid HTTP request.
{% endhint %}



***

## Identifying supported HTTP methods

{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-identifying-and-interacting-with-api-endpoints/api-testing/identifying-supported-http-methods" %}

The HTTP method specifies the action to be performed on a resource. For example:

* `GET` - Retrieves data from a resource.
* `PATCH` - Applies partial changes to a resource.
* `OPTIONS` - Retrieves information on the types of request methods that can be used on a resource.

For example, the endpoint `/api/tasks` may support the following methods:

* `GET /api/tasks` - Retrieves a list of tasks.
* `POST /api/tasks` - Creates a new task.
* `DELETE /api/tasks/1` - Deletes a task.

{% hint style="info" %}
**Note**

When testing different HTTP methods, target low-priority objects. This helps make sure that you avoid unintended consequences, for example altering critical items or creating excessive records.
{% endhint %}



***

## Identifying supported content types



{% embed url="https://portswigger.net/web-security/learning-paths/api-testing/api-testing-identifying-and-interacting-with-api-endpoints/api-testing/identifying-supported-content-types" %}

API endpoints often expect data in a specific format. They may therefore behave differently depending on the content type of the data provided in a request. Changing the content type may enable you to:

* Trigger errors that disclose useful information.
* Bypass flawed defenses.
* Take advantage of differences in processing logic. For example, an API may be secure when handling JSON data but susceptible to injection attacks when dealing with XML.

To change the content type, modify the `Content-Type` header, then reformat the request body accordingly. You can use the Content type converter BApp to automatically convert data submitted within requests between XML and JSON.



***

## Fuzzing to find hidden endpoints

Once you have identified some initial API endpoints, you can fuzz to uncover hidden endpoints. For example, consider a scenario where you have identified the following API endpoint for updating user information:

`PUT /api/user/update`

To identify hidden endpoints, you could use Burp Intruder to fuzz for other resources with the same structure. For example, you could fuzz the `/update` position of the path with a list of other common functions, such as `delete` and `add`.

When fuzzing, use wordlists based on common API naming conventions and industry terms. Make sure you also include terms that are relevant to the application, based on your initial recon.

