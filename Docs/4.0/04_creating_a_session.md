[**Current Version:** 4.0](README.md)

# Creating a Session

### 1. OAuth Flow

...

### 2. Using Credentials to get a Token

To get a token using credentials, an **HTTPS POST** request to `/protocols/login` is used.

Example Body Server Must Expect:
```JSON
{
  "username": "", // username for the user
  "password": "",
  "package": "com.example.app",
  "permissions": {
    "Security": {
      "GenerateSessions": true, // allows client to generate new sessions silently
      "AccessHiddenInformation": true // lets client access hidden account information
    }
  }
}
```

> Clients shouldn't expect server to respect all permissions.
> Server softwares may let users disable some of the permissions.

Response must return token as `plain/text` with `201 Created` status.

This will be used in authorized calls by adding it as `Authorization` header. Example below:

```text
Authorization: Bearer TOKEN
```

### 3. Guest Mode

You can use some endpoints without account; however experience can be less personalized.
To use the Guest account, do not send `Authorization` header.
