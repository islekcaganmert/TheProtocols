[Back](README.md)

# Account Information

## Fetching Account Information

### `org.theprotocols.session.getUserId() -> map`

Call this procedure to get account information of the current user.

Server must return an `org.theprotocols.user` object. No information must be hidden if `org.theprotocols.security.accessHiddenInformation` is granted.

## Editing Account Information

### `org.theprotocols.session.setUserId(string key, any value) -> bool`

To modify a value in account information, **HTTPS POST** request to `/protocols/user_id` is used.

*Networks can be configured to set immutable some of the keys. Client must not expect success everytime.*

Example Body Server Must Expect:

```json
{
  "key": "",
  "data": ""
}
```

Server must return `200 OK` to complete the request.
