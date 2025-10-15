[Back](README.md)

# Editing an Activity

### `net.hereus.sdk.activitypub.edit(string objectId, string summary, string contentWarning, list attachments, map properties, string url) -> null`

Creates a new object with arguments given and publishes a `Create` activity.

### Parameters:

**`objectId` string:** Object to be updated.

**`summary` string:** Text that summarizes the activity. Microblogging software will use this text to visualize it on the feeds.

**`contentWarning` string:** If empty, gets ignored; otherwise, enables `sensitive` bool in the `Note` object and provides the warning text.

**`attachments` list:** URL list of attachments, preferably an attachment uploaded to network via TheProtocols or an IPFS URI.

**`properties` map:** key-value paired data for programmed consumption of the activity.

**`url` string:** URL that "Open in remote instance" will open. If empty, will default to network's social provider, e.g. HereUS Social for HereUS.