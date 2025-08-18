[**Current Version:** 4.0](README.md)

# Account Information

### Fetching Account Information

To get account information of the current user,
an **HTTPS GET** request to `/protocols/account_information` is used.

Server must return an `User` object. No information must be hidden if `Security.AccessHiddenInformation` is granted.

### Editing Account Information

To modify a value in account information, **HTTPS POST** request to `/protocols/account_information` is used.

*Networks can be configured to set immutable some of the keys. Client must not expect success everytime.*

Example Body Server Must Expect:

```json
{
  "key": "",
  "data": ""
}
```

Server must return `200 OK` to complete the request.
