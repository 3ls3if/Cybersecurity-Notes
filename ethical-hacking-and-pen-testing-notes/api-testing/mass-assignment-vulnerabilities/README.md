# 🍷 Mass assignment vulnerabilities

## Mass assignment vulnerabilities

Mass assignment (also known as auto-binding) can inadvertently create hidden parameters. It occurs when software frameworks automatically bind request parameters to fields on an internal object. Mass assignment may therefore result in the application supporting parameters that were never intended to be processed by the developer.



***

## Identifying hidden parameters

Since mass assignment creates parameters from object fields, you can often identify these hidden parameters by manually examining objects returned by the API.

For example, consider a `PATCH /api/users/ request`, which enables users to update their username and email, and includes the following JSON:

{% hint style="info" %}
{

&#x20; "username": "wiener",

&#x20;  "email": "wiener@example.com",

&#x20;}
{% endhint %}

A concurrent `GET /api/users/123` request returns the following JSON:

{% hint style="info" %}
{&#x20;

&#x20; "id": 123, "name": "John Doe",&#x20;

&#x20;  "email": "john@example.com",&#x20;

&#x20;  "isAdmin": "false"

&#x20;}
{% endhint %}

This may indicate that the hidden `id` and `isAdmin` parameters are bound to the internal user object, alongside the updated username and email parameters.



***

## Testing mass assignment vulnerabilities

To test whether you can modify the enumerated `isAdmin` parameter value, add it to the `PATCH` request:

{% hint style="info" %}
{

&#x20; "username": "wiener",&#x20;

&#x20;  "email": "wiener@example.com",&#x20;

&#x20;  "isAdmin": false,&#x20;

}
{% endhint %}

In addition, send a `PATCH` request with an invalid `isAdmin` parameter value:

{% hint style="info" %}
{

&#x20; "username": "wiener",&#x20;

&#x20;  "email": "wiener@example.com",&#x20;

&#x20;  "isAdmin": "foo",&#x20;

}
{% endhint %}

If the application behaves differently, this may suggest that the invalid value impacts the query logic, but the valid value doesn't. This may indicate that the parameter can be successfully updated by the user.

You can then send a `PATCH` request with the `isAdmin` parameter value set to `true`, to try and exploit the vulnerability:

{% hint style="info" %}
{

&#x20; "username": "wiener",&#x20;

&#x20;  "email": "wiener@example.com",&#x20;

&#x20;  "isAdmin": true,&#x20;

}
{% endhint %}

If the `isAdmin` value in the request is bound to the user object without adequate validation and sanitization, the user `wiener` may be incorrectly granted admin privileges. To determine whether this is the case, browse the application as `wiener` to see whether you can access admin functionality.

