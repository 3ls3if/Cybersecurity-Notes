# 🛣 Testing for server-side parameter pollution in REST paths

A RESTful API may place parameter names and values in the URL path, rather than the query string. For example, consider the following path:

```
/api/users/123
```

The URL path might be broken down as follows:

* `/api` is the root API endpoint.
* `/users` represents a resource, in this case `users`.
* `/123`represents a parameter, here an identifier for the specific user.

Consider an application that enables you to edit user profiles based on their username. Requests are sent to the following endpoint:

```
GET /edit_profile.php?name=peter
```

This results in the following server-side request:

```
GET /api/private/users/peter
```

An attacker may be able to manipulate server-side URL path parameters to exploit the API. To test for this vulnerability, add path traversal sequences to modify parameters and observe how the application responds.

You could submit URL-encoded `peter/../admin` as the value of the `name` parameter:

```
GET /edit_profile.php?name=peter%2f..%2fadmin
```

This may result in the following server-side request:

```
GET /api/private/users/peter/../admin
```

If the server-side client or back-end API normalize this path, it may be resolved to `/api/private/users/admin`.
