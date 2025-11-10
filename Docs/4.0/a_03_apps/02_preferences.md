[Back](README.md)

# App Data

### `org.theprotocols.application.getPreferencesLastUpdate() -> integer`

Gets the timestamp for the latest save operation done for the preferences, providing a way to pre-check for changes before fetching again.

### `org.theprotocols.application.getPreferences() -> map`

Gets preferences as a map.

### `org.theprotocols.application.savePreferences(map preferences) -> null`

Saves preferences from a map.

### Limitations and Implementation Requirements

Apps can save preferences up to **4 MB total**. Apps must follow this limitation strictly. Networks are required to reject any save that exceeds limits in order to avoid abuse of the feature.

Implementers should be aware that these preferences are directly customizable by the user via any settings client. Apps must provide all preferences over these procedures unless app's intervention is required for the functionality with no other option.