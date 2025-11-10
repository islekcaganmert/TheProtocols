[Back](README.md)

# Creating a Session

> First method must be preferred as much as possible, and second method must be used where first method is not viable solution.

## 1. Using OAuth

To create a session, user must access the web page on [`org.theprotocols.network().authorizationUrl`](01_network.md)—web apps and PWAs must redirect or create pop-up, and other apps must utilize system provided pop ups or webviews. Network will provide the authorization interface to the user

## 2. Using Credentials

### `org.theprotocols.session.create(string packageName, string username, string password) -> string`

Call this procedure to acquire a session token using credentials.

Before calling, clients must call [`org.theprotocols.network()`](01_network.md) to test network availability.

**Timeout must be disabled,** to let networks to provide necessary security mechanisms to users.
Networks are recommended not to implement security methods that would halt apps. While there is no standard mid-point on this, both clients and servers **must optimize as much as possible**, and servers must implement timeouts for security methods that returns no token.

`packageName` is a reverse domain, e.g. `com.example.application`

Server must return the session token.
