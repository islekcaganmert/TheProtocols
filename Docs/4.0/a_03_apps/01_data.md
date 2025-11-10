[Back](README.md)

# App Data

### `org.theprotocols.application.getData(string name) -> bytes`

Gets the data blob from the name. Name can have slashes to implement folder-like structure, dots to implement blob naming over the package naming, or any other character available in strings.

### `org.theprotocols.application.saveData(string name, bytes data) -> null`

Saves a data blob, overwrites if already exists.

### Limitations and Implementation Requirements

Apps can save up to **256 items** with a name up to **128 characters**, up to **128 KB/item** (kilobytes per item) and **8 MB total**. Apps must follow the limitations on app data storage strictly. Networks are required to reject any save that pushes a data exceeding limits in order to avoid abuse of the feature.

Implementers should use `org.theprotocols.drive.*` procedures to save app files except configs, keys, indices, metadata, manifests, and other data that are irrelevant to the user. However, documents must be available to the user and must be handled by the app if user has no other app to view. Apps must be designed with interoperability and replaceability on the mind.