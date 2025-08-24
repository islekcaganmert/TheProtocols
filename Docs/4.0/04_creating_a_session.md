[**Current Version:** 4.0](README.md)

# Creating a Session

> It was on purpose to use different verbs for first and second approaches.
> First method must be preferred as much as possible, and second method must be used where first method is not viable solution.

The session token that will be received from any means of authorization will be used in authorized calls by adding it as `Authorization` header. Example below:

```text
Authorization: Bearer TOKEN
```

Users may disable some permissions for some apps. Networks must return `403 Forbidden` to the endpoints that require a permission that are disabled or not granted.

In addition to that, 

### 1. Using OAuth

To create a session, `authorizationUrl` from [`network_information`](03_network_information.md) must be served to the user. Web apps and PWAs must redirect, and other apps must utilize system provided pop ups or webviews. Network will provide the authorization interface to the user

### 2. Using Credentials

To acquire a session token using credentials, an **HTTPS POST** request to `/protocols/login` is used.

Timeout must be disabled, assuming client tests network availability by requesting [`network_information`](03_network_information.md) earlier, to allow networks to provide necessary security mechanisms to users.
Networks are recommended not to implement security methods that would halt apps.

Example Body Server Must Expect:
```JSON
{
  "username": "", // username for the user
  "password": "",
  "package": "com.example.app"
}
```

Response must return token as `plain/text` with `200 OK` status.

### 3. Guest Mode

You can use some endpoints without account; however experience can be less personalized.
To use the Guest account, do not send `Authorization` header.
