[**Current Version:** 4.0](../README.md)

# Remote Procedure Calls

TheProtocols uses a special Remote Procedure Call implementation.

Procedures follow a reverse domain hierarchy. For example, core procedures of TheProtocols are located under `org.theprotocols.*`.

To call a procedure, client must send an **HTTPS POST** request to the network. Path must be the function name after the `/theprotocols/` prefix. To pass any parameter, client must send a JSON with the request body.

Response can be either `string`, `integer`, `float`, `bool`, `char`, `byte`, `list`, `map` (dictionary), or `null`.

### Example:

if `com.example.echo` defined with `com.example.echo(string name) -> string`,

```js
com.example.echo("Hello, World!")
```

must translate into

```plaintext
POST /theprotocols/com.example.echo HTTP/2.0
Authorization: ----------
Content-Type: application/json
Accept: text/plain

{"name": "Hello, World!"}
```

and response should be

```
HTTP/2.0 200 OK
Content-Type: text/plain

Hello, User!
```

> `http/2.0` is recommended but not required.

## Types

- **string:** `text/plain`
- **integer:** `text/plain`, e.g. `0`
- **float:** `text/plain`, e.g. `0.0`
- **bool:** `text/plain`, either `true` or `false`
- **char:** `text/plain` with single char
- **bytes:** `application/octet-stream`
- **list:** `application/json` with a list as root
- **map:** `application/json`
- **null:** 202

## Error

If procedure call fails, response must be as given below:

```plaintext
HTTP/2.0 500 Internal Server Error
Content-Type: application/json

{
    "error": "error text here",
    "code": 0,
    "traceback": [
        {"id": 0, "line": "line of code", "error": "error text"}
    ]
}
```

> `traceback` will be ordered with: most recent last. `id` starts from 0 to keep the order safe.

> For production, `traceback` can be set to `null`.

## Authorization

Not all procedures require a session. In this document, we will assume all of the procedures require an authorization, unless specified otherwise.

### While calling from user's network;

`Authorization` header must have a session token given after `Bearer` prefix.

**Example:**
```plaintext
Authorization: Bearer TOKEN
```

### While calling from other networks;

`Authorization` header must have a cryptographic signature in base64 encoding—signed with user's public Dilithium Mode 2 public key—given after `Signature` prefix and user address.

**Example:**
```plaintext
Authorization: Signature username@example.com SIGNATURE
```

## Permissions

Procedures may require some permissions to work. These permissions must be granted while acquiring a session token, and user may block apps from using some of the permissions even if granted initially. If a procedure fails due to a missing or disabled permission, procedure will return status code `403` with missing or disabled permission as response text.