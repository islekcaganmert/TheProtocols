[**Current Version:** 4.0](README.md)

# App Information

### `/.well-known/app_info.json`

To get details about an app, we can use an HTTP GET request to this path under the domain of the app, which is the reversed version of the package name. Server must respond with status code `200` and a JSON body with keys given below:

- `name` (string) Human-readable name of the app
- `icon` (string) URI for the app icon
- `description` (string)
- `latestVersion` (string)
- `latestBuildNumber` (integer)
- `defaultPreferences` (map) Preferences network will serve before any edit
- `initialPermissions` (list) Permissions that are requested initially, apps may request extra permissions or have permissions revoked

### Example:

Package Name: `com.example.application`

```bash
curl https://application.example.com/.well-known/app_info.json
{
  "name": "Example App",
  "icon": "https://application.example.app/favicon.png",
  "description": "Example TheProtocols-enabled app",
  "latestVersion": "1.0.0",
  "latestBuildNumber": 1,
  "defaultPreferences": {},
  "initialPermissions": []
}
```